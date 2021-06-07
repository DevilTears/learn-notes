# Vue

## Vue生命周期有哪些？什么时候可以获取到页面的dom节点，怎么获取？

> 题目来源：2020.12-百度

- beforeCreate 组件实例刚刚创建，组件属性计算之前，
- created 组件实例创建完成，属性已绑定，但DOM还没生成，$el属性还在
- beforeMount 模板编译/挂载之前
- mounted 模板编译/挂载之后
- beforeDestroy 组件销毁前
- destroyed 组件销毁后

mounted之后可以document.querySelector获取dom节点

## vue中nextTick的实现，结合浏览器事件循环机制说一下

> 题目来源：2020.12-好未来

## vm.$nextTick的使用场景

在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

Vue 在修改数据后，视图不会立刻更新，而是等同一事件循环中的所有数据变化完成之后，再统一进行视图更新。例子：

```js
// 改变数据
vm.message = 'changed'

// 想要立即使用更新后的DOM。这样不行，因为设置message后DOM还没有更新
console.log(vm.$el.textContent) // 并不会得到'changed'

// 这样可以，nextTick里面的代码会在DOM更新后执行
Vue.nextTick(function(){
    console.log(vm.$el.textContent) //可以得到'changed'
})
```

## vue中怎么让css只在这个组件内生效

> 题目来源：2020.12 棒棒糖

加该组件的独有的Class 或者 scoped

## vue中css的scoped是怎么样保证不会污染全局的

> 题目来源：2020.12 棒棒糖

编译结果的css有独有的一串字符串代码data-v-randomText

## scoped想影响下一级组件的方法

> 题目来源：2020.12 棒棒糖

```css
/* >>> */
/* 或者 不加scoped */
.parent-component-class .child-component-class {}
```

## vue中template模版怎么编译渲染成虚拟dom树的

> 题目来源：2020.12-好未来

## \<input v-model="msg" \/\> 不使用v-model语法糖实现

```html
<input :value="msg" @input="e => msg = e.target.value">
```

## vue2双向绑定原理

> 题目来源：2020.12-好未来

### Observer

- 负责把 data 选项中的属性转换成响应式数据
- data 中的某个属性也是对象，把该属性转换成响应式数据
- 数据变化发送通知

```js
// defineReactive 中 // 创建 dep 对象收集依赖
const dep = new Dep()
// getter 中
// get 的过程中收集依赖
Dep.target && dep.addSub(Dep.target)
// setter 中
// 当数据变化之后，发送通知
dep.notify()
```

### Compiler

- 负责编译模板，解析指令/插值表达式
- 负责页面的首次渲染
- 当数据变化后重新渲染视图

### Dependency

- 收集依赖，添加观察者(watcher)
- 通知所有观察者

```js
class Dep {
  constructor () {
    // 存储所有的观察者
    this.subs = []
  }
  // 添加观察者
  addSub (sub) {
    if (sub && sub.update) {
        this.subs.push(sub)
    }
  }
  // 通知所有观察者
  notify () {
    this.subs.forEach(sub => {
        sub.update()
    })
  }
}
```

### Watcher

- 当数据变化触发依赖， dep 通知所有的 Watcher 实例更新视图
- 自身实例化的时候往 dep 对象中添加自己

```js
class Watcher {
  constructor (vm, key, cb) {
    this.vm = vm
    // data 中的属性名称
    this.key = key
    // 当数据变化的时候，调用 cb 更新视图
    this.cb = cb
    // 在 Dep 的静态属性上记录当前 watcher 对象，当访问数据的时候把 watcher 添加到dep 的 subs 中
    Dep.target = this
    // 触发一次 getter，让 dep 为当前 key 记录 watcher this.oldValue = vm[key]
    // 清空 target
    Dep.target = null
  }
  update () {
    const newValue = this.vm[this.key]
    if (this.oldValue === newValue) {
        return
    }
    this.cb(newValue)
  }
}
```

## vue3双向绑定原理

> 题目来源：2020.12-好未来

```js
const isObject = val => val !== null && typeof val === 'object'
const convert = target => isObject(target) ? reactive(target) : target
const hasOwnProperty = Object.prototype.hasOwnProperty
const hasOwn = (target, key) => hasOwnProperty.call(target, key)

export function reactive (target) {
  if (!isObject(target)) return target

  const handler = {
    get (target, key, receiver) {
      // 收集依赖
      track(target, key)
      const result = Reflect.get(target, key, receiver)
      return convert(result)
    },
    set (target, key, value, receiver) {
      const oldValue = Reflect.get(target, key, receiver)
      let result = true
      if (oldValue !== value) {
        result = Reflect.set(target, key, value, receiver)
        // 触发更新
        trigger(target, key)
      }
      return result
    },
    deleteProperty (target, key) {
      const hadKey = hasOwn(target, key)
      const result = Reflect.deleteProperty(target, key)
      if (hadKey && result) {
        // 触发更新
        trigger(target, key)
      }
      return result
    }
  }

  return new Proxy(target, handler)
}

let activeEffect = null
export function effect (callback) {
  activeEffect = callback
  callback() // 访问响应式对象属性，去收集依赖
  activeEffect = null
}

let targetMap = new WeakMap()

export function track (target, key) {
  if (!activeEffect) return
  let depsMap = targetMap.get(target)
  if (!depsMap) {
    targetMap.set(target, (depsMap = new Map()))
  }
  let dep = depsMap.get(key)
  if (!dep) {
    depsMap.set(key, (dep = new Set()))
  }
  dep.add(activeEffect)
}

export function trigger (target, key) {
  const depsMap = targetMap.get(target)
  if (!depsMap) return
  const dep = depsMap.get(key)
  if (dep) {
    dep.forEach(effect => {
      effect()
    })
  }
}

export function ref (raw) {
  // 判断 raw 是否是ref 创建的对象，如果是的话直接返回
  if (isObject(raw) && raw.__v_isRef) {
    return
  }
  let value = convert(raw)
  const r = {
    __v_isRef: true,
    get value () {
      track(r, 'value')
      return value
    },
    set value (newValue) {
      if (newValue !== value) {
        raw = newValue
        value = convert(raw)
        trigger(r, 'value')
      }
    }
  }
  return r
}

export function toRefs (proxy) {
  const ret = proxy instanceof Array ? new Array(proxy.length) : {}

  for (const key in proxy) {
    ret[key] = toProxyRef(proxy, key)
  }

  return ret
}

function toProxyRef (proxy, key) {
  const r = {
    __v_isRef: true,
    get value () {
      return proxy[key]
    },
    set value (newValue) {
      proxy[key] = newValue
    }
  }
  return r
}

export function computed (getter) {
  const result = ref()

  effect(() => (result.value = getter()))

  return result
}
```

## vue3比vue2有过那些优化

> 题目来源：2020.12-好未来

### 响应式系统升级

Vue.js 2.x 中响应式系统的核心 defineProperty

Vue.js 3.0 中使用 Proxy 对象重写响应式系统：

- Proxy可以直接监听整个对象而非属性。
- 可以监听动态新增的属性
- 可以监听删除的属性
- 可以监听数组的索引和 length 属性
- Proxy有13中拦截方法，如ownKeys、deleteProperty、has 等是 Object.defineProperty 不具备的。
- Proxy返回的是一个新对象，我们可以只操作新的对象达到目的，而Object.defineProperty只能遍历对象属性直接修改;

### 编译优化

Vue.js 2.x 中通过标记静态根节点，优化 diff 的过程

Vue.js 3.0 中标记和提升所有的静态根节点，diff 的时候只需 要对比动态节点内容

- Fragments(升级 vetur 插件) • 静态提升
- Patch flag
- 缓存事件处理函数

## 了解vue3相关的一些拓展吗

> 题目来源：2020.12-好未来

## setup的生命周期是在什么时候，那两个钩子之间

> 题目来源：2020.12-好未来

## vue 兄弟组件传值

## Vue组件通信

最层外组件内部嵌套了N层子孙组件，最里层的子孙组件如何拿到最层外组件传递过来的属性？

1. Vuex 或者 EventBus
2. $attrs / $listeners
3. provide / inject

## Hash路由与History路由的区别

## History API相关: pushState/replaceState是否会触发popState事件？

调用history.pushState()或者history.replaceState()不会触发popstate事件. popstate事件只会在浏览器某些行为下触发, 比如点击后退、前进按钮(或者在JavaScript中调用history.back()、history.forward()、history.go()方法)，此外，a 标签的锚点也会触发该事件.

## 什么是Vuex

> 题目来源：2020.12 棒棒糖

用于管理页面的数据状态、提供统一数据操作的生态系统

## Vuex有哪几种状态（方法，属性）及作用

> 题目来源：2020.12 棒棒糖

State、 Getter、Mutation 、Action、 Module

## action为啥要调用mutation来修改state

> 题目来源：2020.12 棒棒糖

Vuex这一限制其实也是出于代码设计考虑，action和mutation各司其事，本质上也是遵守了“单一职责”原则。action可以处理异步的方法，mutation是100%同步，可以查看mutation的变更记录。

## vuex状态保留的方法

> 题目来源：2020.12 棒棒糖

存在cookie或者localStorage中

## 双向绑定和vuex的冲突

input的v-model绑定一个来自于vuex的属性，当用户输入时，v-model会尝试修改这个属性，但这个修改不是在mutation中进行的，会抛出一个错误

例如：

```html
<input v-model="$store.state.msg" />
```

解决方案：

```html
<input :value="$store.state.message" @change="e => $store.commit('updateMessage', e.target.value)">
```

```js
<input v-model="message" />

computed: {
  message: {
    get() {
      return this.$store.state.message
    },
    set(value) {
      this.$store.commit('updateMessage', value)
    }
  }
}
```

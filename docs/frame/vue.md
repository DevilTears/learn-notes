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

## vue2双向绑定原理

> 题目来源：2020.12-好未来

## vue3双向绑定原理

> 题目来源：2020.12-好未来

## vue3比vue2有过那些优化

> 题目来源：2020.12-好未来

## 了解vue3相关的一些拓展吗

> 题目来源：2020.12-好未来

## setup的生命周期是在什么时候，那两个钩子之间

> 题目来源：2020.12-好未来

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

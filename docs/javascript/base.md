# JavaScript

## 基本数据类型和引用数据类型

## call、apply、bind的区别(可手写简单实现)

- call、apply的区别：接受参数的方式不一样。
- bind：不立即执行。而apply、call 立即执行。

### 补充提问bind和new的优先级哪个高

```js
function f() {
  return this;
}

const g = f.bind({ a: 1 });

g();  // {a:1}

const obj = new g();

// instanceof都为true
console.assert(obj instanceof f);
console.assert(obj instanceof g);
```

## new的过程

- 创建一个空对象，将它的引用赋给 this，继承函数的原型。
- 通过 this 将属性和方法添加至这个对象
- 最后返回 this 指向的新对象，也就是实例（如果没有手动返回其他的对象（Object/Function））

### 可以继续提问(会有人背概念，面对实际的问题不能全答对)

```js
function f1() {return 123}
function f2() {return {a: 123}}
function f3() {}
console.log(new f1(), new f2(), new f3())
// f1 {}, {a: 123}, f3 {}
```

## WeakMap与Map的区别

- WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。
- WeakMap的键名所指向的对象，不计入垃圾回收机制。（WeakMap/WeakSet没有遍历的方法的原因：垃圾回收机制什么时候触发是无法预测的，WeakMap/WeakSet如果可以遍历，遍历前后的成员数量可能会不一致）

## Proxy

- set 和 deleteProperty 中需要返回布尔类型的值，
在严格模式下，如果返回 false 的话会出现 Type Error 的异常
- Proxy 中 receiver：Proxy 或者继承 Proxy 的对象，Reflect 中 receiver：如果 target 对象中设置了 getter，getter 中的 this 指向 receiver

## 数组扁平化 flat 方法实现

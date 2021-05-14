# JavaScript

## 防抖和节流是什么意思，各自举例一个场景

> 题目来源：2020.12-百度

## 原型链

> 题目来源：2020.12-百度

## 继承的方法

> 题目来源：2020.12-百度

## 两个构造函数A,B 如何让B继承A的属性

> 题目来源：2020.12-百度

## class如何继承

> 题目来源：2020.12-百度

## 输出页面中有多少个div等标签，并分别统计

> 题目来源：2020.12-百度

## foreach, for...in, for...of的区别

> 题目来源：2020.12-百度

forEach 不能使用break return 结束并退出循环

for in 和 for of 可以使用break return；

for in遍历的是数组的索引（即键名）且遍历原型链上的值，而for of遍历的是数组元素值。

for of遍历的只是数组内的元素，而不包括数组的原型属性method和索引name

所以 for in 更适合遍历对象，for of 适合遍历数组或者类数组。

## try Catch可以捕获promise的异常吗

> 题目来源：2020.12 棒棒糖

异步不可以，try-catch 主要用于捕获异常，注意，这里的异常，是指同步函数的异常，如果 try 里面的异步方法出现了异常，此时catch 是无法捕获到异常的，原因是因为：当异步函数抛出异常时，对于宏任务而言，执行函数时已经将该函数推入栈，此时并不在 try-catch 所在的栈，所以 try-catch 并不能捕获到错误。对于微任务而言，比如 promise，promise 的构造函数的异常只能被自带的 reject 也就是.catch 函数捕获到。

- 解决方法： 换用async/await 或者 window 有全局的错误捕获函数 onerror

同步可以，但是前提是promise没有catch，不会冒泡，只被捕获一次

## ES6都用过那些

> 题目来源：2020.12-百度

- symbol 是一种基本类型。Symbol通过调用symbol函数产生，它接收一个可选的名字参数，该函数返回的symbol是唯一的
  - 用于创建独一无二的值，可做唯一key用于缓存等场景
  - 用于创建类的私有变量,利用symbol属性不能被枚举的特性声明作为私有属性
  - 用来重置对象的属性，比如 Symbol.toStringTag
  - 可实现 Symbol.iterator迭代器， 让普通对象变为可迭代对象
  - 使用Symbol.for(‘xxx’)获取全局的symbol值
- for...of循环可以遍历数组、Set和Map结构、某些类似数组的对象、对象，以及字符串
- set数据结构 类似数组。所有的数据都是唯一的，没有重复的值。它本身是一个构造函数

  ```js
    var s1 = new Set(); // 空Set
    var s2 = new Set([1, 2, 3]); // 含1, 2, 3
  ```

- Map是一组键值对的结构，具有极快的查找速度。

  ```js
    var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
    m.get('Michael'); // 95
  ```

## let，const和var的区别

> 题目来源：2020.12 棒棒糖

- var定义的变量，作用域是整个封闭函数，是全域的；let定义的变量，作用域是在块级或者字块中；
- 变量提升：不论通过var声明的变量处于当前作用于的第几行，都会提升到作用域的最顶部。而let声明的变量不会在顶部初始化，凡是在let声明之前使用该变量都会报错（引用错误ReferenceError）；
- 只要块级作用域内存在let，它所声明的变量就会绑定在这个区域；
- let不允许在相同作用域内重复声明（报错同时使用var和let，两个let）。
- const 用来专门声明一个常量，必须初始化值（赋值）

## 箭头函数的this指向，构造函数的this指向

> 题目来源：2020.12 棒棒糖

- 由于没有对象的或者实例的调用,这就相当于在全局当中打印this,所以this都是指向js的顶级对象window.
- 构造函数当中,我们只需要记住,this指向的是调用它的实例对象.
- 箭头函数其实没有this,所以也不能用作构造函数.箭头函数里面的this和函数或者对象调用没有关联,它的指向默认是定义时所处上下的环境所决定的,逐级向上查找找到最近的函数作用域的this.即是是通过call/apply/bind这些也不能够发生变化的.

## ...拓展运算符，是深拷贝还是浅拷贝

> 题目来源：2020.12 棒棒糖

浅拷贝

## 实现一个深拷贝的函数

> 题目来源：2020.12 棒棒糖

```js
// JSON.parse(JSON.stringify(obj))

function deepCopy(obj) {
  const copy = obj instanceof Array ? [] : {}

  for (let i in obj) {
    if (obj.hasOwnProperty(i)) {
      copy[i] = typeof obj[i] === 'Object' ? deepCopy(obj[i]) : obj[j]
    }
  }

  return copy
}
```

## 实现一个ajax方法

> 题目来源：2020.12-百度

```js
var ajax = new XMLHttpRequest()
ajax.open('get',url)
ajax.send()
ajax.onreadystatechange = function(){
  if(ajax.readyState == 4 && ajax.status === 200){
    // 成功
  }
}
```

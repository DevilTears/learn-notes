# 闭包

## 1

> 题目来源：2020.12-好未来

```js
var a = 1;

function Fn1() {
  var a = 2

  console.log('this.a', this.a, 'a:',a)
}

function Fn2() {
  var a = 10

  Fn1()
}

Fn2() // ?  // this.a 1  a: 2

var Fn3 = function() {
 this.a = 3
}

Fn3.prototype = {
  a: 4
}

var fn3 = new Fn3()

Fn1.call(fn3) // this.a 3  a: 2
```

# 原型链

## 什么是原型链

> 题目来源：2020.12-百度

## 继承的方法有那些

> 题目来源：2020.12-百度

## 两个构造函数A,B 如何让B继承A的属性

> 题目来源：2020.12-百度

## class如何继承

> 题目来源：2020.12-百度

## ES5实现继承

```js
function Sup (name) {
  this.name = name;
}

Sup.prototype.getName = function () {
  console.log(this.name)
}

function Child (name) {
  Parent.call(this, name);
}

Child.prototype = Object.create(Sup.prototype);
Child.prototype.constructor = Child;
```

### 如果提到了Object.create,可以提问Object.create(null) 生成的空对象与{}的区别

# 浅拷贝深拷贝

## 深拷贝VS浅拷贝

深拷贝的各种实现方案

手写简易深拷贝，可看代码实现是否处理了对环状引用结构进行了处理，如果是其他的非普通对象/数组的类型数据该怎么处理(例如Date对象)

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

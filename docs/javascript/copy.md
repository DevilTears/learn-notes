# 浅拷贝深拷贝

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

# Algorithm 算法

## 实现 createObj('a,b,c'); 输出 {a: {b: {c: null}}}

> 题目来源：2020.12-百度-智能办公平台部 一面

```js
function createObj(str) {
  let arr = str.split(',')
  let current = null

  for (let i = arr.length - 1; i >= 0; i--) {
    const temp = {}

    temp[arr[i]] = current

    current = temp
  }

  return current
}

createObj('a,b,c');
```

## 实现 repeat(str, count)

> 题目来源：2020.12-百度-智能办公平台部 一面

- repeat('s', 2) // 返回ss
- repeat('a', 3) // 返回aaa

```js
function repeat(str, count) {
  let result = ''

  for (let i = 0; i < count; i++) {
    result += str
  }

  return result
}

repeat('s', 2) // 返回ss
repeat('a', 3) // 返回aaa
```
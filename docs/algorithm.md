# Algorithm 算法

## 实现函数

```js
// createObj('a,b,c'); // {a: {b: {c: null}}}

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

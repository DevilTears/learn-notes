# 代码运行问题

```js
function createIncrement(i) {
  let value = 0;
  return function increment() {
    value += i;
    console.log(value);
    const message = `Current value is ${value}`;
    return function logValue() {
      console.log(message);
    };
  }
}

const inc = createIncrement(1);
const log = inc(); // 1
inc();             // 2
inc();             // 3
log();             // "Current value is 1"
```

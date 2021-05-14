# 代码运行问题

## Promise类

> 题目来源：2020.12-百度

```js
function test(res) {
  return Promise.resolve(res)
    .then(res => {
      console.log(res += '!');
      return res;
    })
    .then(res => {
      console.log(res += '!');
      return Promise.reject("end"); //此处返回了一个新的promise
    })
    .catch(res => {
      console.log(res);
      return res;  //此处也返回了一个新的resolved的promise
    })
    .then(res => {
      console.log(res += '!');  //肯定会执行了
    });
}
test('hello');
```

## 其他类型

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

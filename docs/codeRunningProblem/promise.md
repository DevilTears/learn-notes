# Promise

## 1

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

# 闭包

## 什么是闭包

函数和函数内部能访问到的变量的总和，就是一个闭包。

```js
// 实现一个once函数
const test = () => {console.log(1)}
const func = once(test)

func() // 打印1
func() // 无打印
func() // 无打印
...
```

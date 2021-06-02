# 请求

## 实现一个ajax方法

> 题目来源：2020.12-百度

```js
var ajax = new XMLHttpRequest()
ajax.open('get',url)
ajax.send()
ajax.onreadystatechange = function(){
  if(ajax.readyState == 4 && ajax.status === 200){
    // 成功
  }
}
```

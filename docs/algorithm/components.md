# 实现组件

## 基本思想

## 写一个评分组件

> 题目来源：2020.12-百度

## 用Vue如何设计一个类似Element UI 中 的MessageBox 组件，请写出大概的设计思路 (不用写代码)

> 题目来源：2020.12-好未来

有如下使用要求:

1. 可以注册到全局
2. 符合在组件中可以如下调用

```js
this.$confirm('title', options).then(res => {
  // 点击确认的逻辑
}).catch(error => {
  // 点击取消的逻辑
})
```

解答：

1. vue文件写一个弹框组件，通过css，transform的方式居中，添加一个confirm方法，可以配置title，options（图标）的自定义配置项，并配置好后打开弹窗，返回一个promise函数，当点击确定时，调用resolve，关闭弹窗，点击取消或者蒙层，调用reject关闭弹窗
2. 注册一个plugin组件，引入时配置调用的指令是$confirm,
3. main.js里App.use(plugin)

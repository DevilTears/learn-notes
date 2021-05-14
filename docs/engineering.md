# 工程化

## 如果要发布到npm的话需要做那些处理

> 题目来源：2020.12-百度

- 文档
- 注释
- 性能优化
- count的最大临界值
- 入参的校验
- 单元测试
- babel兼容性
- esModule

## js模块化的规范有哪些

> 题目来源：2020.12-百度

- commonJs(同步) require,exports,module,global
- AMD (异步模块定义)
- CMD (同步模块定义)
- ESModule (“编译时加载”或者静态加载)

## ESModule和CommonJs的区别

> 题目来源：2020.12-百度

纬度 | CommonJs | ES Module
-- | -- | --
值 | 1. 基本类型：值复制，不共享 2. 引用类型：前拷贝，共享 3.工作空间可以修改引入的值 | 1. 只读导入，动态读取 2. 不可在外部修改引用，但可以调用引用中包含的方法
执行顺序| 1. 检查是否有该模块的缓存 2. 如果有，则使用缓存 3. 如果没有，则执行该模块代码，并缓存 | 1. 检查该模块是否引入过 2. 是，暂时认该模块为{} 3. 否，进入该模块并执行其代码(不做缓存) **import会被提升到最先执行**

> [commonJS 和 ES Module 区别](https://zhuanlan.zhihu.com/p/161015809)

## 怎么做埋点，记录看了什么元素，停留时间

> 题目来源：2020.12 棒棒糖

intersectionObserver

```js
var io = new IntersectionObserver(callback, option);

// 开始观察
io.observe(document.getElementById('example'));
// 停止观察
io.unobserve(element);
// 关闭观察器
io.disconnect();
```

callback函数的参数（entries）是一个数组，每个成员都是一个IntersectionObserverEntry对象。

```js
callback: entries => {}
```

IntersectionObserverEntry包含的属性

- time：可见性发生变化的时间，是一个高精度时间戳，单位为毫秒
- target：被观察的目标元素，是一个 DOM 节点对象
- rootBounds：根元素的矩形区域的信息，getBoundingClientRect()方法的返回值，如果没有根元素（即直接相对于视口滚动），则返回null
- boundingClientRect：目标元素的矩形区域的信息
- intersectionRect：目标元素与视口（或根元素）的交叉区域的信息
- intersectionRatio：目标元素的可见比例，即intersectionRect占boundingClientRect的比例，完全可见时为1，完全不可见时小于等于0

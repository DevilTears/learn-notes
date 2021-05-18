# 埋点

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

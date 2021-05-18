# flex

## flex参数align-items等

> 题目来源：2020.12 棒棒糖

flex-direction 主轴方向
justify-content 主轴排列
align-items 副轴排列
flex-wrap 换行

## flex布局，左侧定宽，右侧怎么撑起

> 题目来源：2020.12 棒棒糖

```css
.container {
    width: 100%;
    display: flex;
    flex-flow: row nowrap;
}
.left {
    width: 200px;
    height: 200px;
    background: green;
}
.right {
    flex: 1;
    height: 200px;
    background: red;
}
```

## flex：1是那几个属性的缩写，这几个属性的区别是什么

> 题目来源：2020.12 棒棒糖

- flex-basis basis英文意思是<主要成分>，所以他和width放在一起时,肯定把width干掉，basis遇到width时就会说我才是最主要的成分，你是次要成分，所以见到我的时候你要靠边站。
- flex-grow grow英文意思是<扩大，扩展，增加>,这就代表当父元素的宽度大于子元素宽度之和时，并且父元素有剩余，这时，flex-grow就会说我要成长，我要长大，怎么样才能成长呢，当然是分享父元素的空间了。见下面第二个属性的内容
- flex-shrink shrink英文意思是<收缩，>，这就代表当父元素的宽度小于子元素宽度之和时，并且超出了父元素的宽度，这时，flex-shrink就会说外面的世界太苦了，我还是回到父亲的怀抱中去吧！因此，flex-shrink就会按照一定的比例进行收缩。见下面第三个属性的内容

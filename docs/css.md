# CSS

## css盒式模型

> 题目来源：2020.12 棒棒糖

页面是有无数个盒子组成，每个盒子包括内容（content）、内边距（padding）、边框（border）、外边距（margin）

解析模式：box-sizing

- content-box  元素的宽度/高度由border + padding + content的宽度/高度决定，设置width/height属性指的是content部分的宽/高
- border-box  让元素维持IE传统盒模型（IE6以下版本和IE6~7的怪异模式）。设置width/height属性指的是border + padding + content
- inherit  继承父级

## 元素居中

> 题目来源：2020.12 棒棒糖

```css
/*方法一：使用flex布局*/
/*加入边框和宽高便于浏览器测试*/
.parent {
    border: 1px solid black;
    display:flex;
    justify-content: center;
    align-items: center;
}
.child {
    border: 1px solid black;
    width: 400px;
    height: 400px;
}
/*方法二：绝对定位，左右都是50%，margin-left和top分别为自身一半值的负数*/
.parent {
    position: relative;
}
.child {
    border: 1px solid black;
    width: 400px;
    height: 200px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -200px;
    margin-top: -100px;
}
/*方法三：还是绝对定位，但使用transform*/
.parent{
    position: relative;
}
.child {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

## 左右布局：左边定宽右边自适应

> 题目来源：2020.12 棒棒糖

```css
/* 方法一（使用CSS3的flex布局） */
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

/* 方法二(使用CSS3的calc()，注意calc表达式中的减号前后有空格) */
.left {
    float: left;
    width: 200px;
    height: 200px;
    background: green;
}
.right {
    float: left;
    width: calc(100% - 200px);
    height: 200px;
    background: red;
}

/* 方法三（不设置宽度，默认填充满） */
.left {
    float: left;
    width: 200px;
    height: 200px;
    background: green;
}
.right {
    margin-left: 200px;
    height: 200px;
    background: red;
}

/* 方法四（绝对定位，注意right部分） */
.left {
    position: absolute;
    width: 200px;
    height: 200px;
    background: green;
}
.right {
    position: absolute;
    left: 200px;
    right: 0px;
    height: 200px;
    background: red;
}

/* 方法五(百分比width，这个方法不是很好使，百分比不好确定) */
.left {
    float: left;
    width: 200px;
    height: 200px;
    background: green;
}
.right {
    float: left;
    width: 85%;
    height: 200px;
    background: red;
}
```

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

## 画一个三角形

> 题目来源：2020.12 京东

```css
.triangle{
  width: 0px;
  height: 0px;
  border-bottom: 200px solid #00a3af;
  border-left: 200px solid transparent;    /*transparent 表示透明*/
  border-right: 200px solid transparent;
  /* border-top: 200px solid #00a497;
  border-bottom: 200px solid #cc7eb1;
  border-left: 200px solid #165e83;
  border-right: 200px solid #c85179; */
}
```

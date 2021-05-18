# 布局类问题

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

# 实现

## 画一条 0.5px 的线

1. transform: scale()
2. 添加 meta 标签

    ```html
    <meta name="viewport" content="width=device-width,initial-scale=0.5,user-scalable=0">
    ```

3. 渐变 background: -webkit-linear-gradient(90deg, #000 50%, transparent 50%);

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

## 垂直居中

1. flex + align-items: center
2. position: absolute; top/left: 50%; transform: translate(-50%, -50%); 自身

## 多行省略号

overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;

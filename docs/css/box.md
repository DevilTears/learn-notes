# 盒式模型

> 题目来源：2020.12 棒棒糖

页面是有无数个盒子组成，每个盒子包括内容（content）、内边距（padding）、边框（border）、外边距（margin）

解析模式：box-sizing

- content-box  元素的宽度/高度由border + padding + content的宽度/高度决定，设置width/height属性指的是content部分的宽/高
- border-box  让元素维持IE传统盒模型（IE6以下版本和IE6~7的怪异模式）。设置width/height属性指的是border + padding + content
- padding-box（CSS3添加，火狐私有）设置width/height属性指的是 content + padding
- inherit  继承父级

## inline-block、inline和block的区别；为什么img是inline还可以设置宽高

block: 可设置宽高、padding、margin，前后有换行符
inline-block：可设置宽高、margin、padding 都生效，前后无换行符
inline：设置宽高无效、margin 在垂直方向不生效，padding都有效，前后无换行符

# 循环

## foreach, for...in, for...of的区别

> 题目来源：2020.12-百度

forEach 不能使用break return 结束并退出循环

for in 和 for of 可以使用break return；

for in遍历的是数组的索引（即键名）且遍历原型链上的值，而for of遍历的是数组元素值。

for of遍历的只是数组内的元素，而不包括数组的原型属性method和索引name

所以 for in 更适合遍历对象，for of 适合遍历数组或者类数组。

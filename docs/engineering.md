# 工程化

## 如果要发布到npm的话需要做那些处理

> 题目来源：2020.12-百度-智能办公平台部 一面

- 文档
- 注释
- 性能优化
- count的最大临界值
- 入参的校验
- 单元测试
- babel兼容性
- esModule

## js模块化的规范有哪些

> 题目来源：2020.12-百度-智能办公平台部 一面

- commonJs(同步) require,exports,module,global
- AMD (异步模块定义)
- CMD (同步模块定义)
- ESModule (“编译时加载”或者静态加载)

## ESModule和CommonJs的区别

> 题目来源：2020.12-百度-智能办公平台部 一面

纬度 | CommonJs | ES Module
-- | -- | --
值 | 1. 基本类型：值复制，不共享 2. 引用类型：前拷贝，共享 3.工作空间可以修改引入的值 | 1. 只读导入，动态读取 2. 不可在外部修改引用，但可以调用引用中包含的方法
执行顺序| 1. 检查是否有该模块的缓存 2. 如果有，则使用缓存 3. 如果没有，则执行该模块代码，并缓存 | 1. 检查该模块是否引入过 2. 是，暂时认该模块为{} 3. 否，进入该模块并执行其代码(不做缓存) **import会被提升到最先执行**

> [commonJS 和 ES Module 区别](https://zhuanlan.zhihu.com/p/161015809)
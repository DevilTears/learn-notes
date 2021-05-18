# 异常处理

## try Catch可以捕获promise的异常吗

> 题目来源：2020.12 棒棒糖

异步不可以，try-catch 主要用于捕获异常，注意，这里的异常，是指同步函数的异常，如果 try 里面的异步方法出现了异常，此时catch 是无法捕获到异常的，原因是因为：当异步函数抛出异常时，对于宏任务而言，执行函数时已经将该函数推入栈，此时并不在 try-catch 所在的栈，所以 try-catch 并不能捕获到错误。对于微任务而言，比如 promise，promise 的构造函数的异常只能被自带的 reject 也就是.catch 函数捕获到。

- 解决方法： 换用async/await 或者 window 有全局的错误捕获函数 onerror

同步可以，但是前提是promise没有catch，不会冒泡，只被捕获一次

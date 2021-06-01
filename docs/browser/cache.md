# 缓存

## 浏览器缓存，从Url进入后执行了什么？页面过期时间等（css\js脚本加载）

> 题目来源：2020.12-百度

根据输入地址的域名解析DNS找到服务器地址，发起请求………

> 参考文献：
> [缓存](https://mp.weixin.qq.com/s/7U-poWxaq3ZuBXQJOAtrtQ)

## HTTP请求的缓存，哪两种缓存

> 题目来源：2020.12-百度、2020.12-好未来

- 强缓存
- 协商缓存

## 浏览器的缓存

> 题目来源：2020.12 棒棒糖、2020.12-好未来

- cookie英文饼干，顾名思义，大小应该非常小，cookie非常小，它的大小限制在4kb左右，是网景公司的前雇员在1993年发明。它的主要用于保存登陆信息，比如你登陆某个网站市场可以看到'记住密码’,这就是通过在cookie中存入一段辨别用户身份的数据来实现的。
- localStorage是HTML5标准中新加入的技术，当然早在IE6时代就有一个userData的东西用于本地存储，而当时考虑到浏览器的兼容性，更通用的方案是使用flash。如今localStorage被大多数浏览器所支持。
- sessionStorage与localStorage的接口类似，但保存数据的生命周期与localStorage不同，做过后端的同学都知道Session这个词，翻译过来就是会话。而sessionStorage是前端的一个概念。它只是可以将一部分数据在当前会话中保存下来，刷新页面数据依旧存在。但是叶敏啊关闭后，sessionStorage中的数据就会被清空。

### localStorage、sessionStorage 和 cookie

1. 生命周期：
  a. localStorage 不会过期，除非主动删除
  b. session 存在同窗口、同源，当页面被关闭后被销毁
  c. cookie 在设置的过期时间之前都是有效的

2. 大小
  a. localStorage 一般为5M
  b. session 一般为5M
  c. cookie 4k 左右，而且浏览器对同一域名下存储的 cookie 个数有限制，一般为 20个， 如果超过上限，会随机的覆盖某个已存在的 cookie

3. 共享性
  a. localStorage 不同浏览器无法共享，相同浏览器的不同页面可以共享
  b. session 不同浏览器无法共享，不同页面和标签也不能共享
  c. cookie 4k 左右，而且浏览器对同一域名下存储的 cookie 个数有限制，一般为 20个， 如果超过上限，会随机的覆盖某个已存在的 cookie

4. 占用资源
  cookie 会在浏览器和服务端之间来回传递，占用带宽

### 同一个浏览器打开两个同源页面，其中一个网页修改了localStorage，另一个网页怎么进行监听？

“当同源页面的某个页面修改了localStorage，其余的同源页面只要注册了storage事件，就会触发”

window.addEventListener('storage', (e) => {
  // ...
})

## 强缓存和协商缓存

1. 强缓存：通过 http 头信息来控制，header 中会有两个字段来表明失效规则（expires / cache-control）,指的当前资源的有效期
    a. expires：服务端返回的资源过期时间，浏览器在该时间段内会直接使用缓存，无需再次请求。不过 expires 是 http 1.0 的内容，浏览器现在默认是 http 1.1，因此它的作用基本可以忽略。缺点：expires 的时间是服务端的时间，但是比较的时间，却是客户端的时间，因此一定存在一些差异。

    b. cache-control：代替了 1.0 中的 expires。它指的也是当前资源的有效期。但是它解决了 expires 时间不准确的问题。它下发的是当前资源有效期的相对时间，可以理解为倒计时。cache-control 有用相应头有：
        i. max-age=\[s\]:表示在这个相对时间内，无需重新请求资源
        ii. public: 标记认证的相应才能被缓存
        iii. no-cache：每次使用缓存前都会向服务端验证，当前缓存是否需要更新，保证内容必须是新的。
        IV. no-store：从不使用缓存

2. 对比缓存：进行判断后，决定是否使用缓存。浏览器第一次请求资源时，服务器会将缓存标识与数据一起返回。再次请求数据时，浏览器将上一次的缓存标识一起带上，服务端经过比较后，返回304 或者 200。缓存标识有：
    a. last-modified 与 if-modified-since：服务端下发 last-modified 最后修改时间，浏览器再次请求时带上 if-modified-since（它的值就是服务器上次下发的 last-modified），服务端通过比较资源更改时间 与 last-modified-since，判断是否需要更新

    b. eTag 与 if-none-match：服务器资源唯一标识（eTag = hash(fileName + fileSize + fileUpdateTime)），请求资源时带上 eTag 来比较是否需要更新。eTag 优化了 last-modified，因为last-modified 以秒为单位，如果 1s 内多次更改，那么它的最后编辑时间将不会更新。

## 移动端离线缓存怎么实现的

> 题目来源：2020.12-好未来

离线缓存可以将站点的一些文件缓存到本地，它是浏览器自己的一种机制，将需要的文件缓存下来，以便后期即使没链接网络，被缓存的页面也可以展示

离线缓存的优势：提高用户的访问速度，节省流量；

- 如何实现离线缓存

1. 在需要缓存文件的根节点 html 上添加 manifest 属性（属性值是以 cache.appcache  为后缀的文件）
2. 服务器必须在同级目录下添加以  .appcache为后缀的文件
3. cache.appcache文件的内容

  内容为 ：

  ```cache
  CACHE MANIFEST

  # 1.0  版本号  （这个注释是给 开发者看的，代表了第几个版本）

  CACHE:

  在这里书写需要被缓存的文件，既可以是相对路径，也可以使用绝对路径

  NETWORK:

  *指的是不会被缓存的文件,* 代表 上面的除了上面的缓存文件之外的其他所有都不会被缓存

  FALLBACK:

  如果无法建立英特网请求（如404），而打开的文件
  ```

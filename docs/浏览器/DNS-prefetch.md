### 什么是 DNS

DNS 是什么-- Domain Name System，域名系统，作为域名和 IP 地址相互映射的一个分布式数据库。

**DNS Prefetching**: 浏览器根据自定义的规则，提前去解析后面可能用到的域名，来加速网站的访问速度。简单来讲就是提前解析域名，以免延迟。

```js
<link rel="dns-prefetch" href="//wq.test.com">

// OR

<meta http-equiv="x-dns-prefetch-control" content="on">
```

1. DNS Prefetching 是提前加载域名解析的，省去了解析时间。a 标签的 href 是可以在 chrome、firefox 包括高版本的 IE，但是在 HTTPS 下面不起作用，需要 meta 来强制开启功能
2. 这是 DNS 的提前解析，并不是 css，js 之类的文件缓存，大家不要混淆了两个不同的概念。
3. 如果直接做了 js 的重定向，或者在服务端做了重定向，没有在 link 里面手动设置，是不起作用的。
4. 这个对于什么样的网站更有作用呢，类似 taobao 这种网站，你的网页引用了大量很多其他域名的资源，如果你的网站，基本所有的资源都在你本域名下，那么这个基本没有什么作用。因为 DNS Chrome 在访问你的网站就帮你缓存了。

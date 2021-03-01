---
title: 前端页面性能优化
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/optimization.png'
date: 2019-10-03 11:34:59
summary: 前端页面性能优化
cover: true
tags:
- 优化
---

页面优化以及方向

<!-- more -->

## 1.资源压缩合并，减少Http请求
- 合并图片，css,js文件合并，css,js压缩
- 图片较多可以使用lazyLoad(懒加载)等技术优化
- 使用精灵图，SVG图片，或iconfont等

## 2.非核心代码异步加载

{% folding cyan blue, 异步加载的方式(不含框架，只是原理) %}
1.动态脚本加载
2.defer
3.async
{% endfolding %}

1动态脚本加载：
使用document.createElement创建一个script标签，即document.createElement‘script′，在需要的时候调用。

``` bash
<script>
document.createElement("<script src='a.js'><\/script>");
</script>
``` 

2.defer
通过异步的方式加载defer1.js文件：

``` bash
<script>
<script src="./defer1.js" defer></script>
</script>
``` 

3async：

``` bash
<script>
<script src="./async1.js" async></script>
</script>
``` 

{% span red, defer和async的区别： %}
- defer：在HTML解析完之后才会执行。如果是多个，则按照加载的顺序依次执行。
- async：在加载完之后立即执行。如果是多个，执行顺序和加载顺序无关。

## 3.利用浏览器缓存

浏览器在加载资源时，先根据这个资源的一些http header判断它是否命中强缓存，强缓存如果命中，浏览器直接从自己的缓存中读取资源，不会发请求到服务器。
比如某个css文件，如果浏览器在加载它所在的网页时，这个css文件的缓存配置命中了强缓存，浏览器就直接从缓存中加载这个css，连请求都不会发送到网页所在服务器；
缓存分为：
- 强缓存
- 协商缓存

当强缓存没有命中的时候，浏览器一定会发送一个请求到服务器，通过服务器端依据资源的另外一些http header验证这个资源是否命中协商缓存，如果协商缓存命中，服务器会将这个请求返回，但是不会返回这个资源的数据，而是告诉客户端可以直接从缓存中加载这个资源，于是浏览器就又会从自己的缓存中去加载这个资源。

强缓存与协商缓存的共同点是：如果命中，都是从客户端缓存中加载资源，而不是从服务器加载资源数据；区别是：强缓存不发请求到服务器，协商缓存会发请求到服务器。

当协商缓存也没有命中的时候，浏览器直接从服务器加载资源数据。

## 4.使用CDN

怎么最快地让用户请求资源。一方面是让资源在传输的过程中变小，另外就是CDN。
要注意，浏览器第一次打开页面的时候，浏览器缓存是起不了作任何用的，使用CDN，效果就很明显。

## 5.DNS预解析（dns-prefetch）

通过 DNS 预解析来告诉浏览器未来我们可能从某个特定的 URL 获取资源，当浏览器真正使用到该域中的某个资源时就可以尽快地完成 DNS 解析。

1.打开或关闭DNS预解析
你可以通过在服务器端发送 X-DNS-Prefetch-Control 报头。或是在文档中使用值为 http-equiv 的meta标签：

``` bash
    <meta http-equiv="x-dns-prefetch-control" content="on">
``` 

需要说明的是，在一些高级浏览器中，页面中所有的超链接 {% span red, a %} 标签，默认打开了DNS预解析。但是，如果页面中采用的https协议，很多浏览器是默认关闭了超链接的DNS预解析。如果加了上面这行代码，则表明强制打开浏览器的预解析。（如果你能在面试中把这句话说出来，则一定是你出彩的地方）

2.对指定的域名进行DNS预解析
如果我们将来可能从  {% span red, https://github.com %} 获取图片或音频资源，那么可以在文档顶部的 标签中加入以下内容：

``` bash
    <link rel="dns-prefetch" href="https://github.com">
``` 

当我们从该 URL 请求一个资源时，就不再需要等待 DNS 解析的过程。该技术对使用第三方资源特别有用。    
---
title: 前端页面性能优化
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/logo-horizontal.svg'
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
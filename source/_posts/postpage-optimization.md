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
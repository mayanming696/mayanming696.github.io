---
title: 浅谈RESET.CSS
date: 2021-03-31 10:58:57
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/reset.png'
summary: CSS3
cover: true
tags:
- CSS3
---

{% note quote, 大部分时候,作为前端我们写CSS样式时候都会重置一些默认样式，就有了引入reset.css(早期),大部分都是没有仔细 查看。%}
<!-- more -->

## RESET.CSS发现

这是我今天在百度搜索第一的reset.css文件复制的代码，甚至我的项目大部分样式重置也是大多数这样(惭愧)。
``` bash
/* v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
h1, h2, h3, h4, h5, h6 {
    font-size: 100%;
    font-weight: normal;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

我们引入的 {% span blue, reset.css文件 %}的作用是为了不同浏览器再默认样式上的差别(特别是IE浏览器)，但是现在浏览器在这方面的区别真的比较小了，可是看到有些RESET文件代码还是特别的多

## RESET.CSS(存在的问题)

现在认真看这样的样式，发现很多问题总结两点

{% folding cyan blue, 1.为了统一方便,多做了一些无用功 %}
例如块级元素根本没存在margin,padding
甚至一些项目都不怎么出现的标签都存在了
之前说过前端优化的,压缩代码,冗余代码这样徒增太多(积少成多)
{% endfolding %}

{% folding cyan blue, 2.甚至将一些标签存在的意义都去除 %}
例如，h1~h6 标签的语义网页中的标题，如果去除了默认的加粗样式上跟p,span样式上没有区别个人感觉不妥当。
{% endfolding %}

##  Normalize.css

发现这个样式重置比较规范,而且都有注解

{% btn regular, Normalize.css, https://necolas.github.io/normalize.css/5.0.0/normalize.css/,fas fa-download %}

## 使用样式重置

真正适合项目的，才是合适的这里并不是说一定要用{% span red, Normalize.css文件 %}，也不是说{% span blue, Normalize.css文件 %}就一定比 {% span blue, reset.css文件 %} 好。
只是相同条件下，可是Normalize.css 也并不是所有的样式重置我们真实项目就一定用到，那对于项目来说还是冗余代码。
适合项目团队的配置过合适的修改的才是最好的。

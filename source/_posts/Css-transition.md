---
title: CSS动画效果
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/css.png'
date: 2021-01-27 15:06:23
summary: CSS动画效果
cover: true
tags:
- CSS3
---

{% note quote, 真实项目需要引用一些效果(前端交互)，手写完后感觉还可以就想多了解下遇到大神的博客详解，我想跟自己说我想做一个切图仔。%}

<!-- more -->

先上大神的信息
{% link ChokCoco, https://www.cnblogs.com/coco1s, https://pic.cnblogs.com/avatar/608782/20160411131806.png %}
{% link ChokCoco(Github), https://github.com/chokcoco, https://pic.cnblogs.com/avatar/608782/20160411131806.png %}

## 自己手写的动画效果

``` bash
	/* // 点击效果 */
	.waves {
		position: relative;
		overflow: hidden;
		-webkit-tap-highlight-color:transparent;
	}
	.waves:after {
		content: "";
		display: block;
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		pointer-events: none;
		background-image: radial-gradient(circle, #fff 10%, transparent 10.01%);
		background-repeat: no-repeat;
		background-position: 50%;
		transform: scale(10, 10);
		opacity: 0;
		transition: transform .3s, opacity .5s ease-out;
	}
	
	.waves.dark-waves:after{
		background-image: radial-gradient(circle, #333 10%, transparent 10.01%);
	}
	
	.waves:active:after {
		transform: scale(0, 0);
		opacity: .3;
		transition: 0s;
	}
```

![真实项目点击效果](wavesButton.gif)

{% codepen mayanming696 NWbKjjg dark [ 300] %}
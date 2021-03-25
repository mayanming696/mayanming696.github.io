---
title: Html各标签水平垂直居中方法
date: 2021-03-25 15:36:25
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/center.png'
summary: Html
cover: true
tags:
- Html
---

标签水平垂直居中全攻略，我一定要把你居中。
业务经常遇到一定死要你水平垂直居中。
我来解决。
<!-- more -->

## 行内元素(文本，图片)居中

{% span blue, 行内元素水平居中 %}

给父容器设置：

``` bash
text-align: center;
```


{% span blue, 行内元素垂直居中 %}

给父容器设置行高：

``` bash
.father{
    height:100px；
    line-height:100px
}
```

## 块级元素水平垂直居中

### margin

{% span blue, 块级元素水平居中 %}

margin:auto；即使父元素以及子元素都是设置高度于宽度，只能做到水平（左右）居中，而无法做到水平垂直居中


### 绝对定位 + margin

{% span blue, 子元素需要设定高度 %}

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .father{
            position: relative;
            height: 500px;
            background: red;
        }
        .son {
            position: absolute;
            width: 200px;
            height: 100px;
            background: blue;
            top: 50%;
            left: 50%;
            margin-top: -50px;//需要计算自身高度一半
            margin-left: -100px;//需要计算自身宽度一半
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son">子元素的内容</div>
    </div>
    <script></script>
</body>
</html>
}
```

{% span red, 缺点： %}子元素还要自己偏移自身高度以及宽度50%，手动计算并且还需要子元素设定宽高值

### 绝对定位 + translate(推荐)

{% span blue, 无需指定子元素的宽高，本人超级常用 %}

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .father{
            position: relative;
            height: 500px;
            background: pink;
        }
        .son {
            position: absolute;
            background: red;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son">子元素的内容</div>
    </div>
    <script></script>
</body>
</html>
```


{% span red, 超级推荐： %}子元素使用百分比来设定偏移量，并且子元素不需要设定宽高

### flex 布局

{% span blue, 代码简单,子元素全部水平垂直居中 %}

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .father{
            display: flex; //flex布局
            justify-content: center; //水平居中
            align-items: center; //垂直居中
            min-height: 100vh;
            background: pink;
        }
        .son {
            background: red;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son">子元素的内容</div>
    </div>
    <script></script>
</body>
</html>
```

{% span red, 缺点 %}代码虽然简单，不过父元素里面的所有子元素都是居中的

### flex + margin:auto(推荐)

{% span blue, 推荐，可以指定子元素居中 %}

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .father{
            display: flex;
            min-height: 100vh;
            background: pink;
        }
        .son {
            margin: auto;
            background: red;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son">子元素的内容，想水平垂直居中</div>
        <div class="son2">这个元素不想水平垂直居中</div>
    </div>
    <script></script>
</body>
</html>
```

{% span red, 推荐 %}CSS3 基本都能支持现在的项目使用此方法居中简单

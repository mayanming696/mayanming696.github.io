---
title: JSNumber
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/jsnumber.png'
date: 2021-03-05 09:40:35
summary: JavaScript详解
cover: true
tags:
- JavaScript
---

记录某次真实项目需要计算高精度浮点数，原生JS进行高浮点数计算出现偏差大。

<!-- more -->

## 项目背景

在JS中，整数的运算{% span red,基本简单 %}可以保证精确；但是{% span red,小数的运算，可能会得到一个不精确的结果 %}。所以，千万不要使用JS进行对精确度要求比较高的运算。

例如最简单的测试例子：

``` bash
    var textNumber = 0.1 + 0.2;
    console.log(textNumber);  //打印结果：0.30000000000000004
``` 

具体根本原因：计算机在做运算时，所有的运算都要转换成二进制去计算。然而，有些数字转换成二进制之后，无法精确表示，因此存在浮点数的计算不精确的问题。

## JS处理精度数字运算方法

{% folding cyan open, 1.JS处理精度浮点数运算方法 %}

如果需要的计算结果不需要特别高精度可以 {% span red,toFix() %} 对浮点数进行截取。在进行计算。

{% endfolding %}

{% folding cyan open, 2.JS处理精度浮点数运算方法 %}

在实际中，浮点数计算精确度复杂，因此对数学运算精确度使用开源库，例如：[decimal.js](https://github.com/MikeMcl/decimal.js/) ,[math.js](https://github.com/josdejong/mathjs)。这些都是开源并且比较成熟，直接使用。

- Math.js：属于很全面的运算库，文件很大，压缩后的文件就有500kb。如果你的项目涉及到大型的复杂运算，可以使用 Math.js。
- decimal.js：属于轻量的运算库，压缩后的文件只有32kb。大多数项目的数学运算，使用 decimal.js 足够了。

{% endfolding %}
在使用这两个个开源库时，既可以用 cdn 的方式引入，也可以用 npm 包的方式引入。

### decimal.js语法例子

``` bash
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body>
        <script src="https://cdn.bootcdn.net/ajax/libs/decimal.js/10.2.0/decimal.min.js"></script>
        <script>
            console.log('加法：');
            var a = 0.1;
            var b = 0.2;
            console.log(a + b);
            console.log(new Decimal(a).add(new Decimal(b)).toNumber());

            console.log('减法：');
            var a = 1.0;
            var b = 0.7;
            console.log(a - b);
            console.log(new Decimal(a).sub(new Decimal(b)).toNumber());

            console.log('乘法：');
            var a = 1.01;
            var b = 1.003;
            console.log(a * b);
            console.log(new Decimal(a).mul(new Decimal(b)).toNumber());

            console.log('除法：');
            var a = 0.029;
            var b = 10;
            console.log(a / b);
            console.log(new Decimal(a).div(new Decimal(b)).toNumber());
        </script>
    </body>
</html>
``` 

### math.js语法例子

``` bash
math.add( ) 加

math.subtract( )减
math.divide( ) 除

math.multiply( )乘

``` 
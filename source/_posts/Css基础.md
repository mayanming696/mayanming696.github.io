---
title: CSS基础
date: 2019-10-22 14:39:05
top: false
cover: false
toc: true
mathjax: true
password:
summary: Web前端-(CSS样式)
tags:
- Web前端
categories:
- Web前端样式学习
---

# 一.字体属性和文本属性

---

## CSS 单位

html中的单位只有一种，那就是像素px，所以单位是可以省略的，但是在CSS中不一样。 CSS中的单位是必须要写的，因为它没有默认单位。

* PX ：像素
* em : 印刷单位相当于12个点
* % : 百分比，相对周围的文字的大小
百分比%这个相对单位这里也举个例子：

![](1.png)

---

## font 字体属性

CSS中，有很多非布局样式（与布局无关），包括：字体、行高、颜色、大小、背景、边框、滚动、换行、装饰性属性（粗体、斜体、下划线）等。

CSS样式中，常见的字体属性有以下几种：

        p{
            font-size: 50px; 	       //文本字体大小
            line-height: 30px;         //行高
            font-family: 幼圆,黑体;     //字体类型：如果没有幼圆就显示黑体，没有黑体就显示默认
            font-style: italic ;	   //italic表示斜体，normal表示不倾斜
            font-weight: bold;	       //字体的粗细
            font-variant: small-caps;  //小写变大写     
        }

---

## 行高

为了严格保证字在行里面居中，我们的工程师有一个约定： 行高、字号，一般都是偶数。这样可以保证，它们的差一定偶数，就能够被2整除。

![](3.png)
 
**如何让单行文本垂直居中**

如果一段文本只有一行，如果此时设置行高 = 盒子高，就可以保证单行文本垂直居中。这个很好理解。

上面这个小技巧，只适用于单行文本垂直居中，不适用于多行。如果想让多行文本垂直居中，还需要计算盒子的padding。

**vertical-align: middle; 属性**

        vertical-align: middle; /*指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。*/

---

## 文本属性

        letter-spacing: 1cm ; 单个字母之间的间距
        word-spacing: 1cm; 单词之间的间距
        text-decoration: none; 字体修饰：none 去掉下划线、underline 下划线、line-through 中划线、overline 上划线
        text-transform: lowercase; 单词字体大小写。uppercase大写、lowercase小写
        color:red; 字体颜色
        text-align: center; 在当前容器中的对齐方式。属性值可以是：left、right、center（在当前容器的中间）、justify
        text-transform: lowercase; 单词的字体大小写。属性值可以是：uppercase（单词大写）、lowercase（单词小写）、capitalize（每个单词的首字母大写）

## 列表属性        

![](5.jpg)

---

**overflow属性**

overflow属性的属性值可以是：

* visible：默认值。多余的内容不剪切也不添加滚动条，会全部显示出来。
* hidden：不显示超过对象尺寸的内容。
* auto：如果内容不超出，则不显示滚动条；如果内容超出，则显示滚动条。
* scroll：Windows 平台下，无论内容是否超出，总是显示滚动条。Mac 平台下，和 auto 属性相同。

**鼠标的属性 cursor**

auto：默认值。浏览器根据当前情况自动确定鼠标光标类型。
pointer：IE6.0，竖起一只手指的手形光标。就像通常用户将光标移到超链接上时那样。
hand：和pointer的作用一样：竖起一只手指的手形光标。就像通常用户将光标移到超链接上时那样。

        p:hover{
            cursor: pointer;
        }

---

# 二.背景属性

## 背景常见属性

* background-color:#ff99ff;   //元素的背景颜色
* background-image:url(images/jpg.);   //将图像设置为背景
* background-repeat: no-repeat;    //设置背景图片是否重复及如何重复，默认平铺满（重要）
    * no-repeat不要平铺；
    * repeat-x横向平铺；
    * repeat-y纵向平铺。
* background-position:center top;   //设置背景图片在当前容器中的位置
* background-attachment:scroll;    //设置背景图片是否跟着滚动条一起移动。 scroll(会移动)  fixed(固定不跟着滚动)
* 综合属性叫做background，它的作用是：将上面的多个属性写在一个声明中。

---

## background-color

背景颜色的表示方法有三种：单词、rgb表示法、十六进制表示法
* 用英语单词表示
    比如红色、绿色等。代码举例：

        background-color: red;

* RGB 表示法
    个像素都是由三原色的发光原件组成的，靠明亮度不同调成不同的颜色的。r、g、b的值，每个值的取值范围0~255
    
        background-color: rgb(255,0,0);

* RGBA 表示法

     background-color: rgba(0, 0, 255, 0.3);

* 十六进制表示法
PS:所有用#开头的值，都是16进制的。

    background-color: #ff0000;


* HSLA 表示法

    background-color: hsla(240,50%,50%,0.4);

H 色调，取值范围 0~360。0或360表示红色、120表示绿色、240表示蓝色。
S 饱和度，取值范围 0%~100%。值越大，越鲜艳。
L 亮度，取值范围 0%~100%。亮度最大时为白色，最小时为黑色。
A 透明度，取值范围 0~1。

关于设置透明度的其他方式：

**（1）opacity: 0.3; 会将整个盒子及子盒子设置透明度。也就是说，当盒子设置半透明的时候，会影响里面的子盒子。**
**（2）background: transparent; 可以单独设置透明度，但设置的是完全透明（不可调节透明度）。**

---

## background-repeat属性

background-repeat:no-repeat;设置背景图片是否重复及如何重复，默认平铺满。属性值可以是：
* no-repeat（不要平铺）
* repeat-x（横向平铺）
* repeat-y（纵向平铺）
* 不加这个属性时：（即默认时背景图片会被平铺满）
**padding的区域也是有背景图的。**

---

## background-position属性

background-position属性指的是背景定位属性。公式如下：

在描述属性值的时候，有两种方式：用像素描述、用单词描述

1、用像素值描述属性值：

    格式属性解释
    background-position:向右偏移量 向下偏移量;

属性值可以是正数，也可以是负数

2、用单词描述属性值：

    格式属性解释
    background-position:描述左右的词 描述上下的词;
    1.描述左右的词：left、center、right
    2.描述上下的词：top 、center、bottom

---

## background-size属性：背景尺寸

background-size属性：设置背景图片的尺寸。

格式举例：

    /* 宽、高的具体数值 */
    background-size: 500px 500px;

    /* 宽高的百分比（相对于容器的大小） */
    background-size: 50% 50%;   // 如果两个属性值相同，可以简写成：background-size: 50%;

    background-size: 100% auto;  //这个属性可以自己试验一下。

    /* cover：图片始终填充满容器，且保证长宽比不变。图片如果有超出部分，则超出部分会被隐藏。 */
    background-size: cover;

    /* contain：将图片完整地显示在容器中，且保证长宽比不变。可能会导致容器的部分区域为空白。  */
    background-size: contain;

这里我们对属性值 cover 和 contain 进行再次强调：

cover：图片始终**填充满**容器，且保证**长宽比例不变**。图片如果有超出部分，则超出部分会被隐藏。

contain：将图片**完整**地显示在容器中，且保证**长宽比例不变**。可能会导致容器的部分区域留白。

![](6.jpg)

在上方代码的基础之上，再加一个 background-position: center属性之后，图片就会在容器里居中显示：

![](7.jpg)

---

## 背景原点：background-origin 属性

background-origin 属性：控制背景从什么地方开始显示。

格式举例：

    /* 从 padding-box 内边距开始显示背景图 */
    background-origin: padding-box;           //默认值

    /* 从 border-box 边框开始显示背景图  */
    background-origin: border-box;

    /* 从 content-box 内容区域开始显示背景图  */
    background-origin: content-box;

如果属性值设置成了border-box，那边框部分也会显示图片。

---

## 渐变：background-image

渐变是CSS3当中比较丰富多彩的一个特性，通过渐变我们可以实现许多炫丽的效果，有效的减少图片的使用数量，并且具有很强的适应性和可扩展性。

渐变分为：

* 线性渐变：沿着某条直线朝一个方向产生渐变效果。

* 径向渐变：从一个中心点开始沿着四周产生渐变效果。

* 重复渐变。

见下图：

![](8.png)

**线性渐变**

格式：

    background-image: linear-gradient(方向, 起始颜色, 终止颜色);

    background-image: linear-gradient(to right, yellow, green);

    方向可以是：to left、to right、to top、to bottom、30deg（指的是顺时针方向30°）。

格式解析：

    <!DOCTYPE html>
    <html>
    <head lang="en">
        <meta charset="UTF-8">
        <title></title>
        <style>
            div {
                width: 500px;
                height: 100px;
                margin: 10px auto;
                border: 1px solid #000;
            }

            /* 语法：
                linear-gradient(方向，起始颜色，终止颜色);
                方向：to left   to right  to top   to bottom 　角度　30deg
                起始颜色
                终止颜色
            */
            div:nth-child(1) {
                background-image: linear-gradient(to right, yellow, green);
            }

            /* 不写方向，表示默认的方向是：从上往下 */
            div:nth-child(2) {
                background-image: linear-gradient(yellow, green);
            }

            /* 方向可以指定角度 */
            div:nth-child(3) {
                width: 100px;
                height: 100px;
                background-image: linear-gradient(135deg, yellow, green);
            }

            /* 0%的位置开始出现黄色，40%的位置开始出现红色的过度。70%的位置开始出现绿色的过度，100%的位置开始出现蓝色 */
            div:nth-child(4) {
                background-image: linear-gradient(to right,
                yellow 0%,
                red 40%,
                green 70%,
                blue 100%);

            }

            /* 颜色之间，出现突变 */
            div:nth-child(5) {
                background-image: linear-gradient(45deg,
                yellow 0%,
                yellow 25%,
                blue 25%,
                blue 50%,
                red 50%,
                red 75%,
                green 75%,
                green 100%
                );
            }

            div:nth-child(6) {
                background-image: linear-gradient(to right,
                #000 0%,
                #000 25%,
                #fff 25%,
                #fff 50%,
                #000 50%,
                #000 75%,
                #fff 75%,
                #fff 100%
                );

            }

        </style>
    </head>
    <body>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    </body>
    </html>

![](8.png)

**径向渐变**

格式：

        background-image: radial-gradient(辐射的半径大小, 中心的位置, 起始颜色, 终止颜色);

	    background-image: radial-gradient(100px at center,yellow ,green);

解释：围绕中心点做渐变，半径是150px，从黄色到绿色做渐变。
中心点的位置可以是：at left right center bottom top。如果以像素为单位，则中心点参照的是盒子的左上角。
当然，还有其他的各种参数。格式举例：

    <!DOCTYPE html>
    <html>
    <head lang="en">
        <meta charset="UTF-8">
        <title></title>
        <style>
            div {
                width: 250px;
                height: 250px;
                border: 1px solid #000;
                margin: 20px;
                float: left;
            }

            /*
                径向渐变：
                radial-gradient（辐射的半径大小, 中心的位置，起始颜色，终止颜色）;
                中心点位置：at  left  right  center bottom  top
            */

            /*辐射半径为100px，中心点在中间*/
            div:nth-child(1) {
                background-image: radial-gradient(100px at center, yellow, green);
            }

            /*中心点在左上角*/
            div:nth-child(3) {
                background-image: radial-gradient(at left top, yellow, green);
            }

            div:nth-child(2) {
                background-image: radial-gradient(at 50px 50px, yellow, green);
            }

            /*设置不同的颜色渐变*/
            div:nth-child(4) {
                background-image: radial-gradient(100px at center,
                yellow 0%,
                green 30%,
                blue 60%,
                red 100%);
            }

            /*如果辐射半径的宽高不同，那就是椭圆*/
            div:nth-child(5) {
                background-image: radial-gradient(100px 50px at center, yellow, green);
            }

        </style>
    </head>
    <body>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    </body>
    </html>

效果：

![](9.png)

---

## clip-path：裁剪出元素的部分区域做展示

clip-path属性可以创建一个只有元素的部分区域可以显示的剪切区域。区域内的部分显示，区域外的隐藏。

虽然clip-path不是背景属性，但这个属性非常强大，但往往会结合背景属性一起使用，达到一些效果。

举例：（鼠标悬停时，放大裁剪的区域）

---

# 三.CSS样式表和选择器

## CSS和HTML结合的方式

CSS和HTML的结合方式有3种：

* 行内样式：在某个特定的标签里采用style属性。范围只针对此标签。
* 内嵌样式表：在页面的head里采用 **&#60;style&#62;**标签。范围针对此页面。
* 引入外部样式表css文件的方式。这种引入方式又分为两种：
    * 1、采用 **&#60;link&#62;**标签。例如：**&#60;link rel = "stylesheet" type = "text/css" href = "a.css">&#60;/link&#62;**
    * 2、采用import，必须写在 **&#60;style>**标签中，并且必须是第一句。例如 **@import url(text.css)** ;
**两种引入样式方式的区别：外部样式表中不能写标签，但是可以写import语句**

## 1.CSS和HTML结合方式一：行内样式

采用style属性。范围只针对此标签适用。
该方式比较灵活，但是对于多个相同标签的同一样式定义比较麻烦，适合局部修改。

    <p style="color:white;background-color:red">今日北极熊吞食星星所以明日有雨</p>

---

## 2.CSS和HTML结合方式二：内嵌样式表

在head标签中加入&#60;style&#62;标签，对多个标签进行统一修改，范围针对此页面。

该方式可以对单个页面的样式进行统一设置，但对于局部不够灵活。

举例：

    <style type="text/css">
        p{
            font-weight: bold;
            font-style: italic;
            color: red;
        }

    </style>

    <body>
        <p>洗白白</p>
        <p style="color:blue">你懂得</p>
    </body>

---

## 3.CSS和HTML结合方式三：引入外部样式表css文件

引入样式表文件的方式又分为两种：

（1）采用&#60;link>标签。例如：&#60;link rel = "stylesheet" type = "text/css" href = "text.css">&#60;/link&#62;

（2）采用import，必须写在 **&#60;style&#62;**标签中，并且必须是第一句。**例如：&#64;import url(text.css)** ;

**两种引入样式方式的区别：外部样式表中不能写标签，但是可以写import语句。**

具体操作如下：

我们先在html页面的同级目录下新建一个a.css文件，那说明这里面的代码全是css代码，此时就没有必要再写&#60;style>标签这几个字了。 text.css的代码如下：

    p{
        border: 1px solid red;
        font-size: 40px;
    }

上方的css代码中，注意像素要带上px这个单位，不然不生效。 然后我们在html文件中通过&#60;link&#62;标签引入这个css文件就行了。
这里再讲一个补充的知识：**&#60;link&#62;**标签的rel属性：。其属性值有以下两种：

stylesheet：定义的样式表
alternate stylesheet：候选的样式表

现在我们来定义3个样式表：

a.css：定义一个实线的黑色边框

    div{
        width: 200px;
        height: 200px;
        border: 3px solid black;
    }

ba.css：蓝色的虚线边框

    div{
        width: 200px;
        height: 200px;
        border: 3px dotted blue;
    }

c.css：来个背景图片

    div{
        width: 200px;
        height: 200px;
        border: 3px solid red;
        background-image: url("1.jpg");
    }

然后我们在html文件中引用三个样式表：

    <link rel = "stylesheet" type = "text/css" href = "a.css"></link>
    <link rel = "alternate stylesheet" type = "text/css" href = "b.css" title="第二种样式"></link>
    <link rel = "alternate stylesheet" type = "text/css" href = "c.css" title="第三种样式"></link>

上面引入的三个样式表中，后面两个样式表作为备选。注意备选的样式表中，title属性不要忘记写，不然显示不出来效果的。现在来看一下效果：（在IE中打开网页）

![](9.gif)

---

# 四.CSS的四种基本选择器

CSS选择器：就是指定CSS要作用的标签，那个标签的名称就是选择器。意为：选择哪个容器。

CSS的选择器分为两大类：基本选择题和扩展选择器。

基本选择器：

* 标签选择器：针对一类标签
* ID选择器：针对某一个特定的标签使用
* 类选择器：针对你想要的所有标签使用
* 通用选择器（通配符）：针对所有的标签都适用（不建议使用）

---

## 1、标签选择器：选择器的名字代表html页面上的标签

标签选择器，选择的是页面上所有这种类型的标签，所以经常描述“共性”，无法描述某一个元素的“个性”。

    p{
        font-size:14px;
    }

上方选择器的意思是说：所有的 **&#60;p&#62;**标签里的内容都将显示14号字体。

**【总结】需要注意的是：**

* （1）所有的标签，都可以是选择器。比如ul、li、label、dt、dl、input。

* （2）无论这个标签藏的多深，一定能够被选择上。

* （3）选择的所有，而不是一个。

---

## 2、ID选择器：规定用#来定义
针对某一个特定的标签来使用，只能使用一次。css中的ID选择器以”#”来定义。

    #mytitle{
        border:3px dashed green;
    }

id选择器的选择符是“#”。

任何的HTML标签都可以有id属性。表示这个标签的名字。这个标签的名字，可以任取，但是：

* （1）只能有字母、数字、下划线。
* （2）必须以字母开头。
* （3）不能和标签同名。比如id不能叫做body、img、a。
另外，特别强调的是：HTML页面，不能出现相同的id，哪怕他们不是一个类型。比如页面上有一个id为pp的p，一个id为pp的div，是非法的！

---

## 3、类选择器：规定用圆点.来定义

针对你想要的所有标签使用。优点：灵活。

css中用.来表示类。举例如下：

    .one{
        width:800px;
    }

和id非常相似，任何的标签都可以携带id属性和class属性。class属性的特点：

* 特性1：类选择器可以被多种标签使用。

* 特性2：同一个标签可以使用多个类选择器。用空格隔开。举例如下：（正确）

        <h3 class="teshu  zhongyao">我是一个h3啊</h3>

（1）不要去试图用一个类名，把某个标签的所有样式写完。这个标签要多携带几个类，共同完成这个标签的样式。

（2）每一个类要尽可能小，有“公共”的概念，能够让更多的标签使用。

我们记住这句话：**类上样式，id上行为**。意思是说，class属性交给css使用，id属性交给js使用。

---

# 五.CSS的高级选择器

高级选择器：

* 后代选择器：用空格隔开
* 交集选择器：选择器之间紧密相连
* 并集选择器（分组选择器）：用逗号隔开
* 伪类选择器

---

## 1、后代选择器: 定义的时候用空格隔开

对于E F这种格式，表示所有属于E元素后代的F元素，有这个样式。空格就表示后代。

后代选择器，就是一种平衡：共性、特性的平衡。当要把某一个部分的所有的什么，进行样式改变，就要想到后代选择器。

后代选择器，描述的是祖先结构。

看定义可能有点难理解，我们来看例子吧。

举例：

    <style type="text/css">
            .div1 p{
                color:red;
            }
    </style>

空格就表示后代。.div1 p 表示.div1的后代所有的p。

这里强调一下：这两个标签不一定是连续紧挨着的，只要保持一个后代的关联即可。也就是说，选择的是后代，不一定是儿子。

举例：

	<style type="text/css">
		h3 b i{
			color:red ;
		}
	</style>

上方代码的意思是说：定义了&#60;h3&#62;标签中的&#60;b&#62;标签中的&#60;i&#62;标签的样式。 同理：h3和b和i标签不一定是连续紧挨着的，只要保持一个后代的关联即可。    

---

## 2、交集选择器：定义的时候紧密相连

定义交集选择器的时候，两个选择器之间紧密相连。一般是以标签名开头，比如div.haha，再比如p.special。

如果后一个选择器是类选择器，则写为div.special；如果后一个选择器id选择器，则写为div#special。

来看下面这张图就明白了：

![](10.png)

注意，交集选择器没有空格。所以，没有空格的div.red（交集选择器）和有空格的div .red（后代选择器）不是一个意思。

---

## 3、并集选择器：定义的时候用逗号隔开

三种基本选择器都可以放进来。

    p,h1,#mytitle,.one{
        color:red;
    }

效果：

![](11.png)

---

# 六.伪类（伪类选择器）

伪类：同一个标签，根据其不同的种状态，有不同的样式。这就叫做“伪类”。伪类用冒号来表示。


---

## 超链接a标签

a标签有4种伪类（即对应四种状态），如下：

* :link “链接”：超链接点击之前
* :visited “访问过的”：链接被访问过之后
* :hover “悬停”：鼠标放到标签上的时候
* :active “激活”： 鼠标点击标签，但是不松手时。

在css中，这四种状态必须按照固定的顺序写：

a:link 、a:visited 、a:hover 、a:active
爱恨准则”：love hate。必须先爱，后恨。

## 动态伪类举例

我们在第一段中描述过，下面这三种动态伪类，针对所有标签都适用。

* :hover “悬停”：鼠标放到标签上的时候
* :active “激活”： 鼠标点击标签，但是不松手时。
* :focus 是某个标签获得焦点时的样式（比如某个输入框获得焦点）

---

# 七.CSS样式表的继承性和层叠性

## CSS的继承性

有一些属性，当给自己设置的时候，自己的后代都继承上了，这个就是继承性。
继承性是从自己开始，直到最小的元素。

* 关于文字样式的属性，都具有继承性。这些属性包括：color、 text-开头的、line-开头的、font-开头的。

* 关于盒子、定位、布局的属性，都不能继承。

---

## CSS的层叠性

层叠性：就是css处理冲突的能力。 所有的权重计算，没有任何兼容问题！
当多个选择器，选择上了某个元素的时候，要按照如下顺序统计权重：
id 选择器
类选择器、属性选择器、伪类选择器
标签选择器、伪元素选择器

因为对于相同方式的样式表，其选择器排序的优先级为：ID选择器 > 类选择器 > 标签选择器

权重相同时则选择靠后的

流程图：

![](12.png)

---

# 八.盒子模型

CSS盒模型和IE盒模型的区别：

在 标准盒子模型中，width 和 height 指的是内容区域的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。

IE盒子模型中，width 和 height 指的是内容区域+border+padding的宽度和高度。

标准盒子模型：

![](13.jpg)

IE盒子模型：

![](14.jpg)

---

# 九.浮动






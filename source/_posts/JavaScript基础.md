---
title: JavaScript基础
date: 2019-11-01 
top: false
cover: false
toc: true
mathjax: true
password:
summary: Javascript
tags:
- Javascript
categories:
- Javascript学习
---


# 01.变量

**变量的概念**

>变量：变量可以用来保存字面量，而且变量的值可以任意改变。

**变量的定义和赋值**

![](1.png)

PS:在JavaScript中，永远都是用var来定义变量（在ES6 之前），这和C、Java等语言不同。

变量要先定义，才能使用。比如，我们不设置变量，直接输出：

    <script type="text/javascript">
        console.log(a);
    </script>

控制台将会报错：

![](2.png)

**变量的数据类型**

JS变量会自动的根据存储内容的类型不同，来决定自己的类型。

**在JS中一共有六种数据类型：**
* **基本数据类型（值类型）：** String 字符串、Number 数值、Boolean 布尔值、Null 空值、Undefined 未定义。
* **引用数据类型（引用类型）：** Object 对象。

注意：内置对象function、Array、Date、RegExp、Error等都是属于Object类型。也就是说，除了那五种基本数据类型之外，其他的，都称之为 Object类型。

**数据类型之间最大的区别：**
* 基本数据类型：参数赋值的时候，传数值。
* 引用数据类型：参数赋值的时候，传地址（修改的同一片内存空间）。

---

## **String 字符串**

注意事项：
* 在JS中，字符串需要使用引号引起来。使用双引号或单引号都可以，但是不要混着用。
* 引号不能嵌套：双引号里不能再放双引号，单引号里不能再放单引号。但是单引号里可以嵌套双引号。
* 转义字符：在字符串中我们可以使用\作为转义字符，当表示一些特殊符号时可以使用\进行转义。

**基本数据类型不能绑定属性和方法**

**1、基本数据类型：**

注意，基本数据类型string是无法绑定属性和方法的。比如说：

    var str = "mayanming";
    str.aaa = 12;
    console.log(typeof str);  //打印结果为：string
    console.log(str.aaa);     //打印结果为：undefined

上方代码中，当我们尝试打印str.aaa的时候，会发现打印结果为：undefined。也就是说，不能给 string 绑定属性和方法。

当然，我们可以打印str.length、str.indexOf ("m") 等等。因为这两个方法的底层做了数据类型转换（临时将 string 字符串转换为 String 对象，然后再调用内置方法)

**2、引用数据类型：**

引用数据类型String是可以绑定属性和方法的。如下：

    var strObj = new String("mayanming");
    strObj.aaa = 123;
    console.log(strObj);
    console.log(typeof strObj);  //打印结果：Object
    console.log(strObj.aaa);

![](11.png)

**在底层，字符串以字符数组的形式保存**

	var str = "mayanming";
	console.log(str.length); // 获取字符串的长度
	console.log(str[2]); // 获取字符串中的第2个字符

上方代码中，smyhvae这个字符串在底层是以["m", "a", "y", "a", "n", "m", "i", "n", "g"]的形式保存的。因此，我们既可以获取字符串的长度，也可以获取指定索引index位置的单个字符。这很像数组中的操作。

## 内置对象 String 的常见方法

**charAt()**

> charAt：返回字符串指定位置的字符。不会修改原字符串。

语法：

    字符 = str.charAt(index);

解释：字符串中第一个字符的下标是 0。如果参数 index 不在 [0, string.length) 之间，该方法将返回一个空字符串。

而且，这里的 str.charAt(index)和str[index]的效果是一样的。

**代码举例：**

    var str = new String("mayanming");

    for (var i = 0; i < str.length; i++) {
        console.log(str.charAt(i));
    }

打印结果：

![](12.png)

上面这个例子一般不用。一般打印数组和json的时候用索引，打印String不建议用索引。

---

**charCodeAt()**

> charCodeAt：返回字符串指定位置的字符的 Unicode 编码。不会修改原字符串。

语法：

    Unicode 编码  = str.charCodeAt(index);

另外，sort()方法其实底层也是用到了charCodeAt()，因为用到了Unicode编码。

---

**String.fromCharCode()**

> String.fromCharCode()：根据字符的 Unicode 编码获取字符。

	var result1 = String.fromCharCode(72);
	var result2 = String.fromCharCode(20013);

	console.log(result1); // 打印结果：H
	console.log(result2); // 打印结果：中

---

**indexOf()/lastIndexOf()**

> indexOf()/lastIndexOf()：获取指定字符的索引。

语法：

    索引值 = str.indexOf(想要查询的字符);

解释：indexOf() 是从前向后索引字符串的位置。同理，lastIndexOf()是从后向前寻找。

作用：可以检索一个字符串中是否含有指定内容。如果字符串中含有该内容，则会**返回其第一次出现的索引**；如果没有找到指定的内容，则返回 -1。

因此可以得出一个技巧：如果获取的索引值为0，说明字符串是以查询的参数为开头的。

---

**concat()**

> concat()：字符串的连接。

语法：

    新字符串 = str1.concat(str2)； //链接两个字符串

**这种方法基本不用，直接把两个字符串相加就好。**
是的，你会发现，数组中也有concat()方法，用于数组的连接。这个方法在数组中用得挺多的。

---

**slice()**

> slice()：从字符串中截取指定的内容。不会修改原字符串，而是将及截取到的内容返回。

语法：

    字符串 = str.slice(开始索引, 结束索引); //两个参数都是索引值。包左不包右。

解释：上面的参数，包左不包右。参数举例如下：

* (2, 5) 截取时，包左不包右。

* (2) 表示从指定的索引位置开始，截取到最后。

* (-3) 表示从倒数第几个开始，截取到最后。

* (1, -1) 表示从第一个截取到倒数第一个。

* (5, 2) 表示前面的大，后面的小，返回值为空。

---

**substring()**

> substring()：从字符串中截取指定的内容。和slice()类似。

语法：

    字符串 = str.substring(开始索引, 结束索引); //两个参数都是索引值。包左不包右。

substring()和slice()是类似的。但不同之处在于：

* substring()不能接受负值作为参数。如果传递了一个负值，则默认使用0。

* substring()还会自动调整参数的位置，如果第二个参数小于第一个，则自动交换。比如说， substring(1, 0)截取的是第一个字符。

---

**substr()**

> substr()：从字符串中截取指定的内容。不会修改原字符串，而是将及截取到的内容返回。

语法：

    字符串 = str.substr(开始索引, 截取的长度);


参数举例：

* (2,4)：从索引值为2的字符开始，截取4个字符。

* (1)：从指定位置开始，截取到最后。

* (-3)：从倒数第几个开始，剪到最后.

* 不包括前大后小的情况。

备注：ECMAscript 没有对 substr() 方法进行标准化，因此不建议使用它。

---

**split() 【重要】**

> split()：将一个字符串拆分成一个数组。

语法：

   数组 = str.split();

备注：split()这个方法在实际开发中用得非常多。一般来说，从接口拿到的json数据中，经常会收到类似于"q, i, a, n"这样的字符串，前端需要将这个字符串拆分成['q', 'i', 'a', 'n']数组，这个时候split()方法就排上用场了。

---

**trim()**

> trim()：去除字符串前后的空白。

---

**replace()**

> replace()：将字符串中的指定内容，替换为新的内容并返回。不会修改原字符串。

语法：

    新的字符串 = str.replace(被替换的内容，新的内容);

代码举例：

    //replace()方法：替换
    var str2 = "Today is fine day,today is fine day !!!"
    console.log(str2);
    console.log(str2.replace("today","tomorrow"));  //只能替换第一个today
    console.log(str2.replace(/today/gi,"tomorrow")); //这里用到了正则，才能替换所有的today


---

**大小写转换**
举例：
    var str = "abcdEFG";

    //转换成小写
    console.log(str.toLowerCase());

    //转换成大写
    console.log(str.toUpperCase());



---

## **数值型：Number**

在JS中所有的数值都是Number类型，包括整数和浮点数（小数）。

**数值范围：**

由于内存的限制，ECMAScript 并不能保存世界上所有的数值。
* 最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
* 最小值：Number.MIN_VALUE，这个值为： 5e-324

如果使用Number表示的变量超过了最大值，则会返回Infinity。
* 无穷大（正无穷）：Infinity
* 无穷小（负无穷）：-Infinity

注意：typeof Infinity的返回结果是number。

**NaN和isNaN()函数：**

（1）NaN：是一个特殊的数字，表示Not a Number，非数值。比如：

    console.log("abc" / 18);  //结果是NaN
    console.log("abc" * "abcd"); //结果是NaN

注意：
* typeof NaN的返回结果是number
* Undefined和任何数值计算的结果为NaN。NaN 与任何值都不相等，包括 NaN 本身。

（2）isNaN() :任何不能被转换为数值的值，都会让这个函数返回 true。

    isNaN(NaN);// true
    isNaN("blue"); // true
    isNaN(123); // false

**浮点数的运算：**

在JS中，整数的运算基本可以保证精确；但是小数的运算，可能会得到一个不精确的结果。所以，千万不要使用JS进行对精确度要求比较高的运算。

**连字符和加号的区别**

总结：
* 键盘上的+可能是连字符，也可能是数字的加号。
* 如果加号两边都是数值，此时是加。否则，就是连字符（用来连接字符串）
* 在变量中加入字符串进行拼接，可以被同化为字符串

---

## **布尔值：Boolean**

true 和 false。主要用来做逻辑判断。

布尔值直接使用就可以了，千万不要加上引号

    var a = true;
    console.log(typeof a);//控制台输出结果：boolean

---

## **null和undefined**

**null：空值**

专门用来表示一个为空的**对象**（例如：var a = null）。注意，专门用来表示**空对象**
* Null类型的值只有一个，就是null。比如：var a = null。
* 使用 typeof 检查一个null值时，会返回object。

**undefined：未定义未赋于**
**声明**了一个变量，但是没有**赋值**（例如：var a;），此时它的值就是undefined。
* Undefined类型的值只有一个，就是undefind
* 使用 type of 检查一个undefined时，会返回undefined。

null和undefined有最大的相似性。看看null == undefined的结果(true)也就更加能说明这点。
但是null === undefined的结果(false)。它们虽然相似，但还是有区别的，其中一个区别是：和数字运算时，10 + null结果为：10；10 + undefined结果为：NaN。
* 任何数据类型和undefined运算都是NaN;
* 任何值和null运算，null可看做0运算。

---

# 02.变量的强制类型转换

将一个数据类型强制转换为其他数据类型，主要转换实是在String,Number,Boolean中,不会吧某个数据类型转换成null 和 undefined,因为这么做没有任何的意义

## 其他的简单类型数据 --> String

**方法一：变量+"" 或者 变量+"abc"**

    var a = 123;  // Number 类型
    console.log(a + '');  // 转换成 String 类型
    console.log(a + 'haha');  // 转换成 String 类型

**方法二：调用toString()方法**

格式如下：

> 变量.toString ()

【重要】该方法**不会影响到原变量**，它会将转换的结果返回。当然我们还可以直接写成a = a.toString()，这样的话，就是直接修改原变量。

注意：null和undefined这两个值没有toString()方法，所以它们不能用方法二。如果调用，会报错。

另外，Number类型的变量，在调用toString()时，可以在方法中传递一个整数作为参数。此时它将会把数字转换为指定的进制，如果不指定则默认转换为10进制。例如：

    var a = 255;
    //对于Number调用toString()时可以在方法中传递一个整数作为参数
    //此时它将会把数字转换为指定的进制,如果不指定则默认转换为10进制
    a = a.toString(2);
    console.log(a);        // 11111111
    console.log(typeof a); // string

**方法三：使用String()函数**

格式如下：

> String ( 变量 )

使用String()函数做强制类型转换时：

* 对于Number和Boolean而言，实际上就是调用toString()方法。
* 但是对于null和undefined，就不会调用toString()方法。它会将 null 直接转换为 "null"。将 undefined 直接转换为 "undefined"。

**prompt ()：用户的输入**

prompt()就是专门用来弹出能够让用户输入的对话框。重要的是：用户不管输入什么，都是字符串。

---

## 其他的数据类型 --> Number

**方式一：使用Number ()函数**

情况一：字符串 --> 数字

* 1.如果字符串中是纯数字，则直接将其转换为数字。
* 2.如果字符串中有非数字的内容，则转换为NaN。（此处可以看到Number()函数的局限性）
* 3.如果字符串是一个空串或者是一个全是空格的字符串，则转换为0。

情况二：布尔 --> 数字

* true 转成 1
* false 转成 0

情况三：null --> 数字

* 结果为：0

情况四：undefined --> 数字

* 结果为：NaN


**方式二：parseInt()：字符串 -> 整数【重要】**

parseInt()是专门用来对付字符串的。
parseInt()还具有以下特性：

* （1）只保留字符串最开头的数字，后面的中文自动消失:

    console.log  (  parseInt( "2017在公众号上写了6篇文章") ) ;  //打印结果：2017

    console.log (  parseInt( "2017.01写了6篇文章") ) ;  //打印结果仍是：2017   （说明只会取整数）

    console.log (  parseInt( "aaa2017.01在公众号上写了6篇文章") ) ;  //打印结果：NaN

* 自动带有截断小数的功能：**取整，不四舍五入**。

    var a = parseInt ( 5.8) + parseInt ( 4.7);

    console.log(a);//输出9

* （3）如果对非String使用parseInt ()或parseFloat ()，它会先将其转换为String然后再操作。

    var a = true;
    console.log ( parseInt(a) );  //打印结果：NaN （因为是先将a转为字符串"true"，然后然后再操作）

    var b = null;
    console.log ( parseInt(b) );  //打印结果：NaN  （因为是先将b转为字符串"null"，然后然后再操作）

    var c = undefined;
    console.log ( parseInt(c) );  //打印结果：NaN  （因为是先将b转为字符串"undefined"，然后然后再操作）

    var d = 168.23;
    console.log ( parseInt(d) );  //打印结果：168  （因为是先将c转为字符串"168.23"，然后然后再操作）

* 带两个参数时，表示进制转换。

**parseFloat ()：字符串 --> 浮点数（小数**

parseFloat ()的作用是：将字符串转换为浮点数。

parseFloat ()和parseInt ()的作用类似，不同的是，parseFloat ()可以获得有效的小数部分。

---

## 转换为 Boolean

将其他的数据类型转换为Boolean，可以使用Boolean()函数。

* 情况一：数字 --> 布尔。除了0和NaN，其余的都是true。

* 情况二：字符串 ---> 布尔。除了空串，其余的都是true。

* 情况三：null和undefined都会转换为false。

* 情况四：对象也会转换为true。

---

# 03.运算符

**运算符的定义和分类**
运算符也叫操作符。通过运算符可以对一个或多个值进行运算，并获取运算结果。

运算符有很多分类，比如：

* 算数运算符

* 自增运算符

* 逻辑运算符

* 赋值运算符

* 关系运算符

* 三元运算符

---

## **算数运算符**

![](3.png)

算数运算符的运算规则：
（1）小括号先算小括号(没有中括号，没有大括号，都是小括号镶嵌)

（2）先算乘除、后算加减。

（3）百分号：等于取余。只关心余数


**算数运算符注意事项：**

* 1.当对非Number类型的值进行运算（包括+、-、*、/）时，会将这些值转换为Number然后再运算。（注：字符串 + Number、字符串 + 字符串是特例3）

* 2.任何值和NaN做运算的结果都是NaN。

* 3.任何的值和字符串做加法运算，都会先转换为字符串，然后再做拼串操作。

* 4.任何值做-、*、/运算时都会自动转换为Number。

---

## 自增和自减

**自增 ++**

自增分为两种：
* a++
* ++a

（1）对于一个变量自增以后，原变量的值会**立即**自增1。也就是说，无论是 a++ 还是++a，都会立即使原变量的值自增1。

（2）**我们要注意的是：**a是变量，而a++和++a是表达式。

那这两种自增，有啥区别呢？区别是：a++ 和 ++a的值不同：（也就是说，表达式的值不同）
* a++的值等于原变量的值（a自增前的值）
* ++a的值等于新值 （a自增后的值）

代码举例：

    var n1=1;
    var n2=10;

    var n = n1++; //n1 = 2 n1++ = 1

    console.log('n='+n);  // 1
    console.log('n1='+n1); //2

    n = ++n1 //n1 = 3  ++n1 =3
    console.log('n='+n); //3
    console.log('n1='+n1); //3

    n = n2--;// n2=9 n2--=10
    console.log('n='+n); //10
    console.log('n2='+n2); //9

    n = --n2; //n2=8 --n2 = 8
    console.log('n='+n); //8
    console.log('n2='+n2); //8

---

**逻辑运算符**

逻辑运算符又三种：
* && 与(且，和的意思)：**全部**都为真，结果才为真
* || 或：只要有**一个**是真，结果就是真。
* ! 非：对一个**布尔值**进行取反

注意事项：
* （1）能参与逻辑运算的，都是布尔值。
* （2）JS中的&& 和||属于短路的与跟或(理解为懒人能偷懒就偷懒)，如果第一个值为false，则不会看第二个值。返回结果也一样 举例：

    && 举例:
    //第一个值为true，会检查第二个值

    true && alert ( "看我出不出来！！" );  // 可以弹出 alert 框

    //第一个值为false，不会检查第二个值

    false && alert ( "看我出不出来！！" ); // 不会弹出 alert 框

    || 举例
    //第一个值为true，会检查第二个值

    true || alert ( "看我出不出来！！" );  // 不会弹出 alert 框

    //第一个值为false，不会检查第二个值

    false || alert ( "看我出不出来！！" ); // 会弹出 alert 框

* （3）如果对非布尔值进行逻辑运算，则会先将其转换为布尔值，然后再操作。举例：

    var a = 10;
    a = !a;

    console.log ( a );  // false
    console.log ( typeof a ); // boolean

---

## 三元运算符
三元运算符也叫条件运算符。

语法：

    条件表达式?语句1:语句2;

**执行的流程：**
条件运算符在执行时，首先对条件表达式进行求值：
* 如果该值为true，则执行语句1，并返回执行结果
* 如果该值为false，则执行语句2，并返回执行结果

---

# 04.流程控制语句（if与switch）

## if语句

if语句又三种形式：

1.条件判断语句
条件成立才执行，如果不成立，那就什么都不做。
格式：

    if(条件成立表达){
        //条件为真，做的事情
    }

2.条件分支语句
格式1：

if(条件成立表达){
        //条件为真，做的事情
    }else{
        //条件为假，做的事情
    }


格式2：

    if(条件1成立表达){
        //条件为1，做的事情
    }else if(条件2成立表达){
        //条件为2，做的事情
    }else if(条件3成立表达){
        //条件为1，做的事情
    }else{
        // 条件1、2、3都不满足时，做的事情
    }

**以上所有语句中，只会执行其中一个条件的，满足则执行一个**



## switch语句(条件分支语句)

格式：

    switch(表达式) {
        case 值1：
            语句体1;
            break;

        case 值2：
            语句体2;
            break;

        ...
        ...

        default：
            语句体 n+1;
            break;
    }

执行流程：

* (1)计算表达式的值，和case依次比较，又对应的值则输出对应语句，遇到break则退出结束，没有遇到break则继续输出
* (2)如果所有case都无法对应：则会执行default语句部分内容

swutch注意的点：

* 情况一，遇到break就结束，而不是遇到defaule ( break作用相当于推出switch语句 )
省略掉break可能会遇到持续输出下面内容
* 情况二，执行到switch的程序末尾才结束
switch 语句的结束与 default 的顺序无关，

---

# 05.循环语句

## for循环

语法：

    for(①初始表达式;②条件表达式;④更新表达式){
        ③语句...
    }

执行顺序：

* 1.执行初始表达式，初始变量(只会执行一次)

* 2.执行条件表达式，判断是否执行循环；
 * 如果为true,执行循环③语句
 * 如果为false,终止循环

* 3.执行更新表达式，更新表达式执行完毕继续重复②



## while循环语句

语法：

    while(条件表达式){
        语句...
    }

执行顺序:
while语句在执行时，先对条件表达式进行求值判断：

* 如果值为true，则执行循环体：

	* 循环体执行完毕以后，继续对表达式进行判断
	* 如果为true，则继续执行循环体，以此类推

* 如果值为false，则终止循环

**如果有必要的话，我们可以使用 break 来终止循环。**

**do...while循环**

语法：

    do{
            语句...
        }while(条件表达式)

执行顺序：
do...while语句在执行时，会先执行循环体：

循环体执行完毕以后，在对while后的条件表达式进行判断：
* 如果结果为true，则继续执行循环体，执行完毕继续判断以此类推
* 如果结果为false，则终止循环

**while循环和 do...while循环的区别**
* while是先判断在进行循环；，do....while是先执行后在判断
do..while最少循环一次，whille就不
是

**break**
* break可以用来退出switch语句或**整个**循环语句
* break会立即终止离它**最近**的那个循环语句。
* 可以为循环语句创建一个label，来标识当前的循环（格式：label:循环语句）。使用break语句时，可以在break后跟着一个label，这样break将会结束指定的循环，而不是最近的。

label的使用

    outer:
    for (var i = 0; i < 5; i++) {
        console.log("外层循环 i 的值：" + i)
        for (var j = 0; j < 5; j++) {
            break outer; // 直接跳出outer所在的外层循环（这个outer是我自定义的label）
            console.log("内层循环 j 的值:" + j);
        }
    }
打印结果：

外层循环 i 的值：0

**continue**

* continue可以用来跳过当次循环。

* 同样，continue默认只会离他最近的循环起作用。

---

# 06.对象的介绍以及对象的基本操作

**对象的作用：封装信息**

对象具有特征**特征(属性)**和**行为(方法)**

## 对象简介

**基本数据类型和引用数据类型对比**

* 基本数据类型：Spring字符串，Number数值，Boolean布尔值，Null空值，Undefined未定义
* 引用数据类型：Object对象；

基本数据类型：
基本数据类型的值是直接保存在**栈内存**中，值于值一直是相互独立不干扰，修改一个变量的话不会影响其他变量

引用类型 ，对象：
只要不是基础的五种数据类型就全部是对象
对象是一个符合数据类型，可以一个对象保存多种类型的数据类型的属性
对象是保存在**堆内存**中，每创建一个新的对象，就会在堆内存中开辟新的空间，**变量保存的是对象的内存地址（对象的引用）**
对象的值(对象的属性)保存在堆内存中，对象的引用(变量)是保存在栈内存中
所以两个变量保存的是一个对象的引用，而改变其中一个属性，则会相互影响

**对象的分类**
1.内置对象：
* 由ES标准中定义的对象，在任何的ES的实现中都可以使用
* 比如：Math、String、Number、Boolean、Function、Object....
2.宿主对象：
* 由JS的运行环境提供的对象，目前来讲主要指由浏览器提供的对象。
* 比如 BOM DOM。比如console、document。
3.自定义对象：
* 由开发人员自己创建的对象

## 对象的基本操作
**创建对象**
使用new关键字调用的函数，是构造函数constructor。构造函数是专门用来创建对象的函数。

**向对象中添加属性**
在对象中保存的值称为属性。

**向对象添加属性的语法：**

    对象.属性名 = 属性值（可以为任意甚至是函数）;

**获取对象的属性**

语法1：

    对象.属性名

**如果获取对象中没有的属性，不会报错而是返回undefined**

语法2：

    对象["属性名"] = 属性值

**重要**：使用[] 这种形式去操作属性，更加的灵活，因为，我们可以在[] 中直接传递一个变量，这样变量值是多少就会读取那个属性。

**修改对象的属性值**

语法：

    对象.属性名 = 新值

**删除对象的属性**

语法：

    delete obj.name;

**in 运算符**
通过该运算符可以检查一个对象中是否含有指定的属性。如果有则返回true，没有则返回false。

语法：
    
    "属性名" in 对象

**遍历对象中的属性：for in**

语法：

    for (var 变量 in 对象) {

        }

解释：对象中有几个属性，循环体就会执行几次。每次执行时，会将对象中的**每个属性的 属性名 赋值给变量**

## 创建自定义对象的几种方法

**方式一：对象字面量**

**对象的字面量**就是一个{}。里面的属性和方法均是**键值对**。

    var o = {
        name: "Marco",
        age: 26,
        isBoy: true,
        sayHi: function() {
            console.log(this.name);
        }
    };

    console.log(o);

控制台输出：

![](6.png)

**方式二：工厂模式**
通过该方法可以大批量的创建对象。


         * 使用工厂方法创建对象
         *  通过该方法可以大批量的创建对象
         */
        function createPerson(name, age, gender) {
            //创建一个新的对象
            var obj = new Object();
            //向对象中添加属性
            obj.name = name;
            obj.age = age;
            obj.gender = gender;
            obj.sayName = function() {
                alert(this.name);
            };
            //将新的对象返回
            return obj;
        }

        var obj2 = createPerson("猪八戒", 28, "男");
        var obj3 = createPerson("白骨精", 16, "女");
        var obj4 = createPerson("蜘蛛精", 18, "女");

**弊端：**
使用工厂方法创建的对象，使用的构造函数都是Object。所以**创建的对象都是Object这个类型，就导致我们无法区分出多种不同类型的对象**。

**方式三：利用构造函数**

        //利用构造函数自定义对象
        var stu1 = new Student("Marco");
        console.log(stu1);
        stu1.sayHi();

        var stu2 = new Student("June");
        console.log(stu2);
        stu2.sayHi();


        // 创建一个构造函数
        function Student(name) {
            this.name = name;    //this指的是构造函数中的对象实例
            this.sayHi = function () {
                console.log(this.name + "加油");
            }
        }
    
打印结果：

![](7.png)


---

# 07.构造函数

**代码引入：**

      // 创建一个构造函数，专门用来创建Person对象
      function Person(name, age, gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.sayName = function() {
          alert(this.name);
        };
      }

      // 创建一个构造函数，专门用来创建 Dog 对象
      function Gg() {}

      var per = new Person("路飞", 18, "男");
      var per2 = new Person("艾斯", 24, "男");
      var per3 = new Person("娜美", 18, "女");

      var dd = new Gg();

**构造函数和普通函数的区别**

构造函数就是一个普通的函数，创建方式和普通函数没有区别，不同的是构造函数习惯上首字母大写。

构造函数和普通函数的区别就是**调用方式**的不同：普通函数是直接调用，而**构造函数需要使用new关键字来调用**。

this的指向也有所不同：
* 1.以函数的形式调用时，this永远都是window。比如fun();相当于window.fun();
* 2.以方法的形式调用时，this是调用方法的那个对象
* 3.以构造函数的形式调用时，this是新创建的那个对象

**new 一个构造函数的执行流程**

* （1）开辟内存空间，存储新创建的对象
* （2）将新建的对象设置为构造函数中的this，在构造函数中可以使用this来引用 新建的对象
* （3）执行函数中的代码（包括设置对象属性和方法等）
* （4）将新建的对象作为返回值返回

因为this指的是new一个Object之后的对象实例。于是，下面这段代码：

    // 创建一个函数
    function createStudent(name) {
        var student = new Object();
        student.name = name;      //第一个name指的是student对象定义的变量。第二个name指的是createStudent函数的参数。二者不一样
        }
        可以改为：

    // 创建一个函数
    function Student(name) {
        this.name = name;       //this指的是构造函数中的对象实例
    }

**类、实例**

使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个**类**。

通过一个构造函数创建的对象，称为该类的**实例**。

**instanceof**

使用 instanceof 可以检查一个对象是否为一个类的实例。

语法如下：

    对象 instanceof 构造函数

如果是，则返回true；否则返回false。

代码举例：

      function Person() {}

      function Dog() {}

      var person1 = new Person();

      var dog1 = new Dog();

      console.log(person1 instanceof Person); // 打印结果： true
      console.log(dog1 instanceof Person); // 打印结果：false

      console.log(dog1 instanceof Object); // 所有的对象都是Object的后代。因此，打印结果为：true

根据上方代码中的最后一行，需要补充一点：**所有的对象都是Object的后代，因此 任何对象 instanceof Object 的返回结果都是true**。

## json的介绍

>对象字面量和json比较像，这里我们对json做一个简单介绍。
JSON：JavaScript Object Notation（JavaScript对象表示形式）。

JSON和对象字面量的区别：JSON的属性必须用双引号引号引起来，对象字面量可以省略。

json举例：

      {
            "name" : "zs",
            "age" : 18,
            "sex" : true,
            "sayHi" : function() {
                console.log(this.name);
            }
        };

另外，对象和json没有长度，json.length的打印结果是undefined。于是乎，自然也就不能用for循环遍历（因为遍历时需要获取长度length）。

**json遍历的方法：**

json 采用 for...in...进行遍历，和数组的遍历方式不同。如下：

    var myJson = {
        "name": "Marco",
        "aaa": 18,
        "bbb": "加油"
    };

    //json遍历的方法：for...in...
    for (var key in myJson) {
        console.log(key);   //获取 键
        console.log(myJson[key]); //获取 值（第二种属性绑定和获取值的方法）
        console.log("------");
    }


---

# 08.原型对象

**原型引入**

        function Person(name, age, gender) {
            this.name = name;
            this.age = age;
            this.gender = gender;
            //向对象中添加一个方法
            this.sayName = function () {
                console.log("我是" + this.name);
            }
        }

        //创建一个Person的实例
        var per = new Person("Marco", 18, "男");
        var per2 = new Person("June", 18, "女");
        per.sayName();
        per2.sayName();

        console.log(per.sayName == per2.sayName);  //打印结果为false

分析如下：
上方代码中，我们的sayName方法是写在构造函数 Person 内部的，然后在两个实例中进行了调用。造成的结果是，**构造函数每执行一次，就会给每个实例创建一个新的 sayName 方法**。也就是说，每个实例的sayName都是唯一的。因此，最后一行代码的打印结果为false。

按照上面这种写法，假设创建10000个对象实例，就会创建10000个 sayName 方法。这种写法肯定是不合适的。我们为何不让所有的对象共享同一个方法呢？

还有一种方式是，将sayName方法在全局作用域中定义：（不建议。原因看注释）

        function Person(name, age, gender) {
            this.name = name;
            this.age = age;
            this.gender = gender;
            //向对象中添加一个方法
            this.sayName = fun;
        }

        //将sayName方法在全局作用域中定义
        /*
         * 将函数定义在全局作用域，污染了全局作用域的命名空间
         *  而且定义在全局作用域中也很不安全
         */
        function fun() {
            alert("Hello大家好，我是:" + this.name);
        };

比较好的方式是，在原型中添加sayName方法：

    Person.prototype.sayName = function(){
        alert("Hello大家好，我是:"+this.name);
    };

**原型prototype的概念**

>我们所创建的每一个函数，解析器都会向函数中添加一个属性 prototype。这个属性对应着一个对象，这个对象就是我们所谓的原型对象。

*认识1：
如果函数作为普通函数调用prototype没有任何作用，当函数以构造函数的形式调用时，它所创建的实例对象中都会有一个隐含的属性，指向该构造函数的原型，我们可以通过__proto__来访问该属性。

代码举例：

	// 定义构造函数
	function Person() {}

	var per1 = new Person();
	var per2 = new Person();

	console.log(Person.prototype); // 打印结果：[object object]

	console.log(per1.__proto__ == Person.prototype); // 打印结果：true

上方代码的最后一行：打印结果表明，实例. __proto__ 和 构造函数.prototype都指的是原型对象。

* 认识2：

原型对象就相当于一个公共的区域，所有同一个类的实例都可以访问到这个原型对象，我们可以将对象中共有的内容，统一设置到原型对象中。

以后我们创建构造函数时，可以将这些对象共有的属性和方法，统一添加到构造函数的原型对象中，这样就不用分别为每一个对象添加，也不会影响到全局作用域，就可以使每个对象都具有这些属性和方法了

* 认识3：

使用 in 检查对象中是否含有某个属性时，如果对象中没有但是**原型中有**，也会返回true。

可以使用对象的hasOwnProperty () 来检查**对象自身中**是否含有该属性。

**原型链访问方法对象的顺序 （ 就近原则 ）**

原型对象也是对象，所以它也有原型，当我们使用或访问一个对象的属性或方法时：

* 它会先在对象自身中寻找，如果有则直接使用；
* 如果没有则会去原型对象中寻找，如果找到则直接使用；
* 如果没有则去原型的原型中寻找，直到找到Object对象的原型。
* Object对象的原型没有原型，如果在Object原型中依然没有找到，则返回 null

---

# 09.函数

函数：就是将一些功能或语句进行**封装**，在需要的时候，通过**调用**的形式，执行这些语句。

* 函数也是对象
* 使用 typeof 检查一个函数对象的时候，返回function

函数的作用：
* 将大量重复的语句动作写在函数里面，之后需要运用的地方进行调用即可，避免了重复的编写
* 专业来说就是简化编程，让编程模块化

## 函数的定义和调用

方式一：使用 **函数声明** 来创建一个函数

	function 函数名([形参1,形参2...形参N]){  // 备注：语法中的中括号，表示“可选”
		语句...
	}

解释如下：
* function：是一个关键字。中文 “函数” “功能”
* 函数名字：命名规范跟变量命名一样，不能数字开头
* 参数：可选
* 大括号里面：是这个函数的语句，行为

方式二：使用 **函数表达式** 来创建一个函数

	var 函数名  = function([形参1,形参2...形参N]){
		语句....
	}

方式二中的函数表达式 ，是将一个匿名函数赋值给一个变量

方式三：使用构造函数创建一个对象，这种方式很少

--- 

## 函数的调用
函数调用的方法：

    函数名字();

**函数的参数：形参和实参**

![](4.png)

**注意：实际参数和形式参数的个数，要相同。**

形参：
* 可以在函数()中指定一个或多个形参
* 多个形参之间用,隔开，声明形参就相当于在函数内部声明了对应的变量，但是不赋值

实参：
* 在调用函数的时候，可以在()中指定实参
* 实参将会赋值给函数中对应的形参
实参的类型：
* 函数的实参可以是任意的数据类型。调用函数时解析器不会检查实参的类型，所以要注意，是否有可能会接收到非法的参数，如果有可能则需要对参数进行类型的检查。
* 实参的数量：调用函数时，解析器也不会检查实参的数量：多余实参不会被赋值。如果实参的数量少于形参的数量，则没有对应实参的形参将是undefined。

---

## 函数的返回值

    console.log(sum(3, 4));

	//函数：求和
	function sum(a, b) {
		return a + b;
	}

return的作用是结束方法
注意：
* return后的值将会作为函数的执行结果返回，可以定义一个变量，来接收该结果。

* 在函数中return后的语句都不会执行（函数在执行完 return 语句之后停止并立即退出）

* 如果return语句后不跟任何值，就相当于返回一个undefined

* 如果函数中不写return，则也会返回undefined

* 返回值可以是任意的数据类型，可以是对象，也可以是函数。

---

## 函数名、函数体和函数加载问题（重要，请记住）
我们要记住：**函数名 == 整个函数**。举例

    console.log(fn) == console.log(function fn(){alert(1)});

    //定义fn方法
    function fn(){
        alert(1)
    };

我们知道，当我们在调用一个函数时，通常使用函数()这种格式；但此时，我们是直接使用函数这种格式，它的作用相当于整个函数。

**函数的加载问题：**JS加载的时候，只加载函数名，不加载函数体。所以如果想使用内部的成员变量，需要调用函数。

---

## fn() 和 fn 的区别【重要】

* **fn ()**：调用函数。相当于获取了函数的返回值。

* **fn**：函数对象。相当于直接获取了函数对象。

---

## 立即执行函数

例子：

        function(a, b) {
            console.log("a = " + a);
            console.log("b = " + b);
        };
        ```


    立即执行函数如下：

        javascript  
        (function(a, b) {
            console.log("a = " + a);
            console.log("b = " + b);
        })(123, 456);

立即执行函数：函数定义完，立即被调用，这种函数叫做立即执行函数。

立即执行函数往往只会执行一次。为什么呢？因为没有变量保存它，执行完了之后，就找不到它了。

---

## 方法

函数也可以称为对象的属性。**如果一个函数作为一个对象的属性保存，那么我们称这个函数是这个对象的方法**。

调用这个函数就说调用对象的方法（method）。相比于方法，它只是名称上的区别，并没有其他的区别。

函数举例：

	// 调用函数
	fn();

方法举例：

	// 调用方法
	obj.fn();

我们可以这样说，如果直接是fn()，那就说明是函数调用。如果是发现XX.fn()的这种形式，那就说明是**方法**调用。    

---

## 类数组 arguments

在调用函数时，浏览器每次都会传递进两个隐含的参数：

* 1.函数的上下文对象 this
* 2.封装实参的对象 arguments

例如：

    function foo() {
        console.log(arguments);
        console.log(typeof arguments);
    }

    foo();

arguments是一个类数组对象，它可以通过索引来操作数据，也可以获取长度。

**arguments代表的是实参**。在调用函数时，我们所传递的实参都会在arguments中保存。有个讲究的地方是：**arguments只在函数中使用**。

**1.返回函数实参的个数：arguments.length**

arguments.length可以用来获取**实参的长度**。

    fn(2,4);
    fn(2,4,6);
    fn(2,4,6,8);

    function fn(a,b) {
        console.log(arguments);
        console.log(fn.length);         //获取形参的个数
        console.log(arguments.length);  //获取实参的个数

        console.log("----------------");
    }

我们即使不定义形参，也可以通过arguments来使用实参（只不过比较麻烦）：arguments[0] 表示第一个实参、arguments[1] 表示第二个实参...

**2、返回正在执行的函数：arguments.callee**

arguments里边有一个属性叫做callee，这个属性对应一个函数对象，就是当前正在指向的函数对象。

    function fun() {

        console.log(arguments.callee == fun); //打印结果为true
    }

    fun("hello");

**3、arguments可以修改元素**

之所以说arguments是伪数组，是因为：arguments可以修改元素，但不能改变数组的长短。举例：

    fn(2,4);
    fn(2,4,6);
    fn(2,4,6,8);

    function fn(a,b) {
        arguments[0] = 99;  //将实参的第一个数改为99
        arguments.push(8);  //此方法不通过，因为无法增加元素
    }

---

# 10.作用域（Scope）的概念

作用域指一个变量的作用范围。在js中，一共有两种作用域：
* 全局作用域
* 函数作用域

## 全局作用域

直接编写在script标签中的JS代码，都在全局作用域。

* 全局作用域在页面打开时创建，在页面关闭时销毁。

* 在全局作用域中有一个全局对象window，它代表的是一个浏览器的窗口，它由浏览器创建我们可以直接使用。

在全局作用域中：

* 创建的变量都会作为window对象的属性保存。

* 创建的函数都会作为window对象的方法保存。

全局作用域中的变量都是全局变量，在页面的任意的部分都可以访问的到。

## 变量提升

使用var关键字声明的变量（ 比如 var a = 1），会在**所有的代码执行之前被声明但是不会赋值**，但是如果**声明变量时不是用var关键字（比如直接写a = 1），则变量不会被声明提前**。

**函数声明提前**

**函数声明：**
使用函数声明的形式创建的函数function foo(){}，会被**声明提前（函数最优先）**。

也就是说，整个函数会在所有的代码执行之前就被**创建完成**，所以我们可以在函数声明之前，调用函数。

在函数中，没有var声明的变量都是全局变量，而且并不会提前声明。

代码举例：

    fn1();  // 虽然 函数 fn1 的定义是在后面，但是因为被提前声明了， 所以此处可以调用函数

    function fn1() {
        console.log('我是函数 fn1');
    }

**函数表达式：**
使用函数表达式创建的函数var foo = function(){}，不会被声明提前，所以不能在声明前调用。

很好理解，因为此时foo被声明了，且为undefined，并没有把 function(){} 赋值给 foo。


![](5.png)

---

## 作用域
**作用域：**变量和函数生效的区域。作用域在**函数定义**时，就已经确定了。

在函数作用域中可以访问到全局作用域的变量，在全局作用域中无法访问到函数作用域的变量。

**执行期上下文**：当**函数执行**时，会创建一个执行期上下文的内部对象。每调用一次函数，就会创建一个新的上下文对象，他们之间是相互独立的。当函数执行完毕，它所产生的执行期上下文会被销毁。

**作用域的上下级关系：**
当在函数作用域操作一个变量时，它会先在自身作用域中寻找，如果有就直接使用（**就近原则**）。如果没有则向上一级作用域中寻找，直到找到全局作用域；如果全局作用域中依然没有找到，则会报错ReferenceError。

在函数中要访问全局变量可以使用window对象。（比如说，全局作用域和函数作用域都定义了变量a，如果想访问全局变量，可以使用window.a）

---

# 11.this

解析器在调用函数每次都会向函数内部传递进一个隐含的参数，这个隐含的参数就是this，this指向的是一个对象，这个对象我们称为函数执行的 上下文对象。

**根据函数的调用方式的不同，this会指向不同的对象：**

* 1.**最终**以**函数**的形式调用时，this永远都是window。比如fun();相当于window.fun();

* 2.**最终**以**方法**的形式调用时，this是调用方法的那个对象

* 3.**最终**以**构造函数**的形式调用时，this是新创建的那个对象

* 4.**最终**使用**call**和**apply**调用时，this是指定的那个对象


**1.举例**

    function fun() {
        console.log(this);
        console.log(this.name);
    }

    var obj1 = {
        name: "smyh",
        sayName: fun
    };

    var obj2 = {
        name: "vae",
        sayName: fun
    };

    var name = "全局的name属性";

    //以函数形式调用，this是window
    fun();       //可以理解成 window.fun()

    **打印结果：**
    Window
    全局的name属性

---

**2.举例**

        function fun() {
            console.log(this);
            console.log(this.name);
        }

        var obj1 = {
            name: "smyh",
            sayName: fun
        };

        var obj2 = {
            name: "vae",
            sayName: fun
        };

        var name = "全局的name属性";

        //以方法的形式调用，this是调用方法的对象
        obj2.sayName();
        
        **打印结果：**
        Object
        vae

---

**3.举例**

    function fn(){
        this.num = 1;
    }

    var a = new fn();

    console.log(a.num); //1

**更新一个小问题当this碰到return时**

    function fn()  
    {  
        this.user = 'Marco';  
        return {};  
    }
    var a = new fn;  
    console.log(a.user); //undefined

---

    function fn()  
    {  
    this.user = 'Marco';  
    return function(){};
    }
    var a = new fn;  
    console.log(a.user); //undefined

---

    function fn()  
    {  
        this.user = 'Marco';  
        return 1;
    }
    var a = new fn;  
    console.log(a.user); //Marco

---

function fn()  
{  
    this.user = 'Marco';  
    return undefined;
}
var a = new fn;  
console.log(a.user); //Marco


**如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。**

---

# 12.数组简介

数组（Array）是属于内置对象，我们可以在MDN网站上查询各种方法。

数组和普通对象的功能类似，也是用来存储一些值的。不同的是：

普通对象是使用字符串作为属性名的，而数组是使用数字来作为索引来操作元素。索引：从0开始的整数就是索引。
数组的存储性能比普通对象要好。在实际开发中我们经常使用数组来存储一些数据，使用频率非常高。

## 数组的基本操作

数组的元素可以是任意的数据类型，也可以是对象，也可以是函数，也可以是数组。

数组的元素中，如果存放的是数组，我们就称这种数组为二维数组。

## 创建数组

* **方法一** : 字面量定义举例：

    var arr = [1,2,3];

* **方法二** ：对象定义(数组的构造函数)
语法：

    var arr = new Array(参数);

如果**参数为空**，则表示创建一个空数组；参数位置是**一个数值**时，表示数组长度；参数位置是**多个数值**时，表示数组中的元素。

    // 方式一
    var arr1 = [11, 12, 13];

    // 方式二
    var arr2 = new Array(); // 参数为空
    var arr3 = new Array(4); // 参数为一个数值
    var arr4 = new Array(15, 16, 17); // 参数为多个数值

    console.log(typeof arr1);  // 打印结果：object

    console.log("arr1 = " + JSON.stringify(arr1));
    console.log("arr2 = " + JSON.stringify(arr2));
    console.log("arr3 = " + JSON.stringify(arr3));
    console.log("arr4 = " + JSON.stringify(arr4));
    打印结果：
    object
    arr1 = [11,12,13]
    arr2 = []
    arr3 = [null,null,null,null]
    arr4 = [15,16,17]

从上方打印结果的第一行里，可以看出，数组的类型其实也是属于**对象**。

---

## **向数组中添加元素**
语法：

    数组[索引] = 值

---

## **获取数组中的元素**
语法：

    数组[索引]

数组的索引代表的是数组中的元素在数组中的位置，从0开始。

如果读取不存在的索引（比如元素没那么多），系统不会报错，而是返回undefined。

代码举例：

    var arr = [21, 22, 23];

    console.log(arr[0]); // 打印结果：21
    console.log(arr[5]); // 打印结果：undefined

---

## **获取数组的长度**

可以使用length属性来获取数组的长度(元素的个数)。

语法：

    数组的长度 = 数组名.length；

代码举例：

    var arr = [21, 22, 23];

    console.log(arr.length); // 打印结果：3

补充：
对于连续的数组，使用length可以获取到数组的长度（元素的个数）；对于非连续的数组，使用length会获取到数组的最大的索引+1。因此，尽量不要创建非连续的数组。

---

## **修改数组的长度（修改length）**
* 如果修改的length大于原长度，则多出部分会空出来，置为 null。
* 如果修改的length小于原长度，则多出的元素会被删除，数组将从后面删除元素。
* 特例：伪数组arguments的长度可以修改，但是不能修改里面的元素

代码举例：

    var arr1 = [11, 12, 13];
    var arr2 = [21, 22, 23];

    // 修改数组 arr1 的 length
    arr1.length = 1;
    console.log(JSON.stringify(arr1));

    // 修改数组 arr2 的 length
    arr2.length = 5;
    console.log(JSON.stringify(arr2));
    打印结果：
    [11]

    [21,22,23,null,null]

---

# 13.数组的常见方法&数组的遍历

**数组的四个基础方法** （数组元素的添加和删除）

|方法       | 描述           | 备注  |
| ------------- |:-------------:| -----:|
| push()      | 向数组的**最后面**插入一个或多个元素，返回**结果为该数组新的长度** | 会改变原数组 |
| pop()      | 删除数组中的**最后一个元素**，返回**结果为被删除的元素**	      |   会改变原数组 |
| unshift() | 在数组**最前面**插入一个或多个元素，返回**结果为该数组新的长度**      |    会改变原数组 |
| shift() | 删除数组中的**第一个元素**，返回**结果为被删除的元素**      |    会改变原数组 |

**数组的常见方法如下：**

|方法       | 描述           | 备注  |
| ------------- |:-------------:| -----:|
| for循环()  |  |  |
| forEach() | 和 for循环类似，但需要兼容IE8以上	|  forEach() 没有返回值。也就是说，它的返回值是 undefined |
| map() | 对原数组中的**每一项**进行加工，将组成**新的数组** | 不会改变原数组 |
| filter() | 对数组中**每一项**运行回调函数，该函数返回结果是true的项，将组成新的数组，**返回结果为新的数组**。可以起到过滤的作用 | 不会改变原数组 |
| every() | 如果有一项返回false，则停止遍历，此方法返回 false | 一假即假。要求每一项都返回true，最终的结果才返回true |
| some() | 只要有一项返回true，则停止遍历，此方法返回true | 一真即真。要求每一项都返回false，最终的结果才返回false |
| reduce | 为数组中的每一个元素，依次执行回调函数   |     |


**数组的其他方法如下：**

|方法       | 描述           | 备注  |
| ------------- |:-------------:| -----:|
| indexOf(value) | 从前往后索引，获取 value 在数组中的第一个下标 |  |
| lastIndexOf(value) | 从后往前索引，获取 value 在数组中的最后一个下标 |  |
| find(function()) | 找出第一个满足「指定条件返回true」的元素。 |  |
| findIndex(function())	 | 找出第一个满足「指定条件返回true」的元素的index |   |
| Array.from(arrayLike)	 | 将伪数组转化为真数组  |  |
| Array.of(value1, value2, value3)	| 将一系列值转换成数组。 |  |

## 数组的四个基本方法（数组元素的添加和删除）

**push()**

> push()：向数组的**最后面插入**一个或多个元素，返回**结果为该数组新的长度**。

语法：

    数组的新长度 = 数组.push(元素);

代码举例：

	var arr = ["Marco", "June", "leslie"];

	var result1 = arr.push("vk"); // 末尾插入一个元素
	var result2 = arr.push("gg", "dd"); // 末尾插入多个元素

	console.log(result1); // 打印结果：4
	console.log(result2); // 打印结果：6
	console.log(JSON.stringify(arr)); // 打印结果：["Marco","June","leslie","vk","gg","dd"]

---

**pop()**

> pop()：**删除**数组中的**最后一个元素**，返回**结果为被删除的元素**。

语法：

    被删除的元素 = 数组.pop();

代码举例：

	var arr = ["王一", "王二", "王三"];

	var result1 = arr.pop();

	console.log(result1); // 打印结果：王三
	console.log(JSON.stringify(arr)); // 打印结果：["王一","王二"]

---

**unshift()**

> unshift()：在数组**最前面**插入一个或多个元素，返回**结果为该数组新的长度**。插入元素后，其他元素的索引会依次调整。

语法：

    数组的新长度 = 数组.unshift(元素);

代码举例：

    var arr = ["王一", "王二", "王三"];

	var result1 = arr.unshift("王四"); // 最前面插入一个元素
	var result2 = arr.unshift("王五", "王六"); // 最前面插入多个元素

	console.log(result1); // 打印结果：4
	console.log(result2); // 打印结果：6
	console.log(JSON.stringify(arr)); // 打印结果：["王五","王六","王四","王一","王二","王三"]

---

**shift()**

> shift()：删除数组中的第一个元素，返回结果为被删除的元素。

语法：

    被删除的元素 = 数组.shift();

代码举例：

	var arr = ["王一", "王二", "王三"];

	var result1 = arr.shift();

	console.log(result1); // 打印结果：王一
	console.log(JSON.stringify(arr)); // 打印结果：["王二","王三"]

---

## 数组的常见方法
**slice()**

> slice()：从数组中提取指定的一个或者多个元素，返回结果为新的数组（不会改变原来的数组）。
备注：该方法不会改变原数组，而是将截取到的元素封装到一个新数组中返回。

语法：

    新数组 = 原数组.slice(开始位置的索引, 结束位置的索引);    //注意：包含开始索引，不包含结束索引

举例：

    var arr = ["a", "b", "c", "d", "e", "f"];

    var result1 = arr.slice(2); //从第二个值开始提取
    var result2 = arr.slice(-2); //提取最后两个元素
    var result3 = arr.slice(2, 4); //提取从第二个到第四个之间的值（不包括第四个值）
    var result4 = arr.slice(4, 2); //空

    console.log("arr:" + JSON.stringify(arr));
    console.log("result1:" + JSON.stringify(result1));
    console.log("result2:" + JSON.stringify(result2));
    console.log("result3:" + JSON.stringify(result3));
    console.log("result4:" + JSON.stringify(result4));
    打印结果：
    arr:["a","b","c","d","e","f"]
    result1:["c","d","e","f"]
    result2:["e","f"]
    result3:["c","d"]
    result4:[]

---

**splice()**

> splice()：从数组中删除指定的一个或多个元素，返回结果为新的数组（会改变原来的数组）。
备注：该方法会改变原数组，会将指定元素从原数组中删除；被删除的元素会封装到一个新的数组中返回。

语法：

    新数组 = 原数组.splice(起始索引index, 需要删除的个数, 第三个参数, 第四个参数...);

上方语法中，第三个及之后的参数，表示：向原数组中添加新的元素，这些元素将会自动插入到开始位置索引的前面。

举例1：

    var arr1 = ["a", "b", "c", "d", "e", "f"];
    var result1 = arr1.splice(1); //从第index为1的位置开始，删除元素

    console.log("arr1：" + JSON.stringify(arr1));
    console.log("result1：" + JSON.stringify(result1));
    打印结果：
    arr1：["a"]
    result1：["b","c","d","e","f"]

举例2：
    var arr2 = ["a", "b", "c", "d", "e", "f"];
    var result2 = arr2.splice(-2); //删除最后两个元素

    console.log("arr2：" + JSON.stringify(arr2));
    console.log("result2：" + JSON.stringify(result2));

    打印结果：
    arr2：["a","b","c","d"]
    result2：["e","f"]

举例3：

    var arr3 = ["a", "b", "c", "d", "e", "f"];
    var result3 = arr3.splice(1, 3); //从第index为1的位置开始删除元素,一共删除三个元素

    console.log("arr3：" + JSON.stringify(arr3));
    console.log("result3：" + JSON.stringify(result3));

    打印结果：
    arr3：["a","e","f"]
    result3：["b","c","d"]

举例4：

    var arr4 = ["a", "b", "c", "d", "e", "f"];

    //从第index为1的位置开始删除元素,一共删除三个元素。并且在 index=1 的前面追加两个元素
    var result4 = arr4.splice(1, 3, "Marco", "vae");

    console.log("arr4：" + JSON.stringify(arr4));
    console.log("result4：" + JSON.stringify(result4));

    打印结果：
    arr4：["a","Marco","vae","e","f"]
    result4：["b","c","d"]

---

**concat()**

> concat()：连接两个或多个数组，返回结果为新的数组。（不会改变原数组）

语法：

    新数组 = 数组1.concat(数组2, 数组3 ...);

举例：

    var arr1 = [1, 2, 3];
    var arr2 = ["a", "b", "c"];
    var arr3 = ["Marco", "vae"];

    var result1 = arr1.concat(arr2);

    var result2 = arr2.concat(arr1, arr3);

    console.log("arr1 =" + JSON.stringify(arr1));
    console.log("arr2 =" + JSON.stringify(arr2));
    console.log("arr3 =" + JSON.stringify(arr3));

    console.log("result1 =" + JSON.stringify(result1));
    console.log("result2 =" + JSON.stringify(result2));

    打印结果：
    arr1 =[1,2,3]
    arr2 =["a","b","c"]
    arr3 =["Marco","vae"]

    result1 =[1,2,3,"a","b","c"]
    result2 =["a","b","c",1,2,3,"Marco","vae"]

从打印结果中可以看到，原数组并没有被修改。

---

**join()**

join()：将数组转换为字符串，返回结果为转换后的字符串（不会改变原来的数组）。
join()方法可以指定一个字符串作为参数，这个字符串将会成为数组中元素的连接符；如果不指定连接符，则默认使用 , 作为连接符，此时和 toString()的效果是一致的。

语法：

    新的字符串 = 原数组.join(参数); // 参数选填

代码举例：

    var arr = ["a", "b", "c"];

    var result1 = arr.join(); // 这里没有指定连接符，所以默认使用 , 作为连接符

    var result2 = arr.join("-"); // 使用指定的字符串作为连接符

    console.log(typeof arr); // 打印结果：object
    console.log(typeof result1); // 打印结果：string

    console.log("arr =" + JSON.stringify(arr));
    console.log("result1 =" + JSON.stringify(result1));
    console.log("result2 =" + JSON.stringify(result2));

    上方代码中，最后三行的打印结果是：

    arr =["a","b","c"]
    result1 =a,b,c
    result2 =a-b-c

---

**reverse()**

> reverse()：反转数组，返回结果为反转后的数组（会改变原来的数组）。

语法：

    反转后的数组  =  数组.reverse();

举例：

    var arr = ["a", "b", "c", "d", "e", "f"];

    var result = arr.reverse(); // 将数组 arr 进行反转

    console.log("arr =" + JSON.stringify(arr));
    console.log("result =" + JSON.stringify(result));

    打印结果：
    arr =["f","e","d","c","b","a"]
    result =["f","e","d","c","b","a"]

从打印结果可以看出，原来的数组已经被改变了。

---

**sort()方法**

>sort()：对数组的元素进行从小到大来排序（会改变原来的数组）。

**sort()方法举例：无参时**
如果在使用 sort() 方法时不带参，则默认按照Unicode编码，从小到大进行排序。

**sort()方法举例：带参时**
如果在 sort()方法中带参，我们就可以**自定义**排序规则。具体做法如下：

我们可以在sort()添加一个回调函数，来指定排序规则。回调函数中需要定义两个形参，浏览器将会分别使用数组中的元素作为实参去调用回调函数

浏览器根据回调函数的返回值来决定元素的排序：（重要）

* 如果返回一个大于0的值，则元素会交换位置
* 如果返回一个小于0的值，则元素位置不变
* 如果返回一个0，则认为两个元素相等，则不交换位置

---

## 数组的遍历

遍历数组即：获取并操作数组中的每一个元素。在我们的实战开发中，使用得非常频繁。

遍历数组的方法包括：every()、filter()、forEach()、map()、some()

PS：这几个方法**不会修改原数组**。

语法格式：

    数组/boolean/无 = 数组.every/filter/forEach/map/some(
                        function(item, index, arr){
                                        程序和返回值；
                        })

---

**for循环 遍历**

        var arr = ["Marco","June","vk"];
        for(var i = 0;i<arr.length;i++){
            console.log(arr[i]);  // arr[i]代表的是数组中的每一个元素i
        }

        console.log(arr);
    

![](8.png)

---

**forEach() 遍历**

> forEach() 这种遍历方法只支持IE8以上的浏览器。IE8及以下的浏览器均不支持该方法。所以如果需要兼容IE8，则不要使用forEach，改为使用for循环来遍历即可。

forEach()方法需要一个函数作为参数。这种函数，是由我们创建但是不由我们调用的，我们称为回调函数。
数组中有几个元素，该回调函数就会执行几次。执行完毕后，浏览器会将遍历到的元素。
回调函数中传递三个参数：
* 第一个参数，就是当前正在遍历的元素
* 第二个参数，就是当前正在遍历的元素的索引
* 第三个参数，就是正在遍历的数组

代码举例：

    var arr = ["Marco", "June", "Vk"];

    arr.forEach(function(item, index, obj) {
    console.log("item:" + item);
    console.log("index:" + index);
    console.log("obj:" + obj);
    console.log("----------");
    });

    打印结果：
    item:Marco
    index:0
    obj:Marco,June,Vk
    ----------

    item:June
    index:1
    obj:Marco,June,Vk
    ----------

    item:Vk
    index:2
    obj:Marco,June,Vk
    ----------

注意，forEach() 的返回值是 undefined。也就是说，它没有返回值。如果你尝试 tempArry = arr.forEach()这种方式来接收，是达不到效果的。

---

**map()方法**

> 解释：对数组中每一项运行回调函数，返回该函数的结果，组成的新数组（返回的是**加工之后**的新数组）。

**举例1：**（拷贝的过程中改变数组元素的值）

有一个已知的数组arr1，我要求让arr1中的每个元素的值都加10，这里就可以用到 map 方法。代码举例：

    var arr1 = [1, 3, 6, 2, 5, 6];

    var arr2 = arr1.map(function (item, index) {
        return item + 10;  //让arr1中的每个元素加10

    })
    console.log(arr2);

    打印结果：
    Array [10, 13, 16, 12, 15, 16];

**举例2：【重要案例，实际开发中经常用到】**
将A数组中某个属性的值，存储到B数组中。代码举例：

    const arr1 = [
        { name: 'Marco', age: '18' },
        { name: 'June', age: '18' },
    ];

    // 将数组 arr1 中的 name 属性，存储到 数组 arr2 中
    const arr2 = arr1.map(item => item.name);

    // 将数组 arr1 中的 name、age这两个属性，改一下“键”的名字，存储到 arr3中
    const arr3 = arr1.map(item => ({
        myName: item.name,
        myAge: item.age,
    })); // 将数组 arr1 中的 name 属性，存储到 数组 arr2 中

    console.log('arr1:' + JSON.stringify(arr1));
    console.log('arr2:' + JSON.stringify(arr2));
    console.log('arr3:' + JSON.stringify(arr3));
    
    打印结果：
    arr1:[{"name":"Marco","age":"18"},{"name":"June","age":"18"}]

    arr2:["Marco","June"]

    arr3:[{"myName":"Marco","myAge":"28"},{"myName":"June","myAge":"32"}]

map的应用场景，主要就是以上两种。

**filter()**
> 解释：对数组中每一项运行回调函数，该函数返回结果是true的项，将组成新的数组（返回值就是这个新的数组）。

**举例1：**找出数组 arr1 中大于4的元素，返回一个新的数组。代码如下：

    var arr1 = [1, 3, 6, 2, 5, 6];

    var arr2 = arr1.filter(function(item, index) {
        return item > 4; //将arr1中大于4的元素返回，组成新的数组
    });
    console.log(JSON.stringify(arr2));

    打印结果：
    [6,5,6]

**举例2：**
获取数组A中指定类型的对象，放到数组B中。代码举例如下：

    var arr1 = [
        { name: '许嵩', type: '一线' },
        { name: '周杰伦', type: '过气' },
        { name: '邓紫棋', type: '一线' },
    ];

    var arr2 = arr1.filter(item => item.type == '一线'); // 筛选出一线歌手

    console.log(JSON.stringify(arr2));

    打印结果：
    [{"name":"许嵩","type":"一线"},{"name":"邓紫棋","type":"一线"}]

---

**every()方法**

> every()：对数组中每一项运行回调函数，如果都返回true，every就返回true；如果有一项返回false，则停止遍历，此方法返回false。
注意：every()方法的返回值是boolean值，参数是回调函数。

举例：

    var arr1 = ["千古", "宿敌", "南山忆", "素颜"];
    var bool1 = arr1.every(function (element, index, array) {
        if (element.length > 2) {
            return false;
        }
        return true;
    });
    console.log(bool1);  //输出结果：false。只要有一个元素的长度是超过两个字符的，就返回false

    var arr2 = ["千古", "宿敌", "南山", "素颜"];
    var bool2 = arr2.every(function (element, index, array) {
        if (element.length > 2) {
            return false;
        }
        return true;
    });
    console.log(bool2);  //输出结果：true。因为每个元素的长度都是两个字符。

---

**some()方法**

> some()：对数组中每一项运行回调函数，只要有一项返回true，则停止遍历，此方法返回true。

注意：some()方法的返回值是boolean值。

---

**reduce()方法**

> reduce()：为数组中的每一个元素，依次执行回调函数。

语法：

    arr.reduce(
        function(previousValue, item, index, arr) {

        }, initialValue)
    
参数解释：

* previousValue：上一次调用回调函数时的返回值，或者初始值

* currentValue：当前正在处理的数组元素

* currentIndex：当前正在处理的数组元素下标

* array：调用reduce()方法的数组

* initialValue：可选的初始值（作为第一次调用回调函数时传给 previousValue 的值）

举例1：

    var arr = [2, 0, 1, 9, 6];
    sumValue = arr.reduce(function(total, item) { //  计算 arr 数组中，所有元素项的综合
        return total + item;
    }, 0);

    console.log('sumValue:' + sumValue); // 打印结果：18

---

## 数组的其他方法

**indexOf() 和 lastIndexOf()：获取数据的索引**

语法：

    索引值 = 数组.indexOf(value);

    索引值 = 数组.lastIndexOf(value);

解释：

* indexOf(value)：从前往后索引，获取 value 在数组中的第一个下标。
* lastIndexOf(value) ：从后往前索引，获取 value 在数组中的最后一个下标。

作用：

利用这个方法，我们可以判断某个值是否在指定的数组中。如果没找到则返回-1。

举例：

    var arr = ["a","b","c","d","e","d","c"];

    console.log(arr.indexOf("c"));       //从前往后，找第一个"c"在哪个位置
    console.log(arr.lastIndexOf("d"));   //从后往前，找第一个"d"在哪个位置

    打印结果：
    2
    5

举例2：判断某个值是否在数组中：

    var arr = ["29926392220", "29965620629", "28003663436", " ", "28818504366"];

    var str = [
        {name:"smyh", id: "12334"},

        {name:"vae", id: "28818504366"}
    ];

    str.filter(item => {
        console.log(arr.indexOf(item.id));
    })

---

**find()**

> 作用：找出第一个满足「指定条件返回true」的元素。

语法：

    find(function(item, index, arr){return true})

举例：

        let arr = [2, 3, 2, 5, 7, 6];

        let result = arr.find(function (item, index) {
            return item > 4; //遍历数组arr，一旦发现有第一个元素大于4，就把这个元素返回
        });

        console.log(result);  //打印结果：5
    
---

**findIndex()**

> 作用：找出第一个满足「指定条件返回true」的元素的index。

语法：

    findIndex(function(item, index, arr){return true})

举例：

    let arr = [2, 3, 2, 5, 7, 6];

    let result = arr.findIndex(function (item, index) {
            return item > 4; //遍历数组arr，一旦发现有第一个元素大于4，就把这个元素的index返回
    });

    console.log(result); //打印结果：3

---

**Array.from()**

> 作用：将伪数组或可遍历对象转换为真数组。

语法：

    array = Array.from(arrayLike)

伪数组与真数组的区别：

伪数组的原型链中没有 Array.prototype，而真数组的原型链中有 Array.prototype。因此伪数组没有 pop、join等属性。

---

**Array.of()**

> 作用：将一系列值转换成数组。

语法：

    Array.of(value1, value2, value3)

举例：

    let arr = Array.of(1, 'abc', true);
    console.log(arr);

---

## 其他
**isArray()：判断是否为数组**

    布尔值 = Array.isArray(被检测的值) ;

以前，我们会通过 A instanceof B来判断 A 是否属于 B 类型。但是在数组里，这种 instanceof 方法已经用的不多了，因为有下面isArray()方法。

---

**toString()：转换数组**

    字符串 = 数组.toString();

> 解释：把数组转换成字符串，每一项用,分割。

---

**valueOf()：返回数组本身**

    数组本身 = 数组.valueOf();

这个方法的意义不大。因为我们指直接写数组对象的名字，就已经是数组本身了。

---

# 14.内置对象

> 内置对象就是指这个语言自带的一些对象，供开发者使用，这些对象提供了一些常用的或是最基本而必要的功能。

## JavaScript的内置对象：

|内置对象       | 对象说明           |
| ------------- |:-------------:|
| Arguments     | 函数参数集合 |
| Array      | 数组	 |
| Boolean | 布尔对象  |
| Date | 日期时间    |
| Error | 异常对象   |
| Function | 函数构造器    |
| Math | 数学对象  |
| Number | 数值对象  |
| Object | 基础对象  |
| RegExp | 正则表达式对象  |
| String | 字符串对象  |

## 内置对象：Date

Date对象的创建:

**写法一：** 表示的是当前代码执行的时间（也可以理解成是获取当前时间对象）

    var date1 = new Date();
    console.log(date1);

**写法二：** 在参数中传递一个表示时间的字符串（兼容性最强）

    var date2 = new Date("2019/12/09 09:00:00");
    console.log(date2);

写法三：（不常用）

    var date3 = new Date('Wed Dec 09 2019 12:00:00 GMT+0800 (中国标准时间)');
    console.log(date3 );

写法四：（不常用）

    var date4 = new Date(2019, 11, 09);    
    console.log(date4);

![](9.png)

---

## 获取日期和时间
Date对象 有如下方法，可以获取日期和时间：

* getDate() 获取日 1-31
* getDay() 获取星期 0-6（0代表周日，1代表周一）
* getMonth() 获取月 0-11（0代表一月）
* getFullYear() 获取年份
* getHours() 获取小时 0-23
* getMinutes() 获取分钟 0-59
* getSeconds() 获取秒 0-59
* getMilliseconds() 获取毫秒 （1s = 1000ms）

代码举例：

	var myDate = new Date();

	console.log(myDate); // 打印结果：Mon Dec 09 2019 11:12:30 GMT+0800 (中国标准时间)
	console.log(myDate.getDate()); // 打印结果：9
	console.log(myDate.getDay()); // 打印结果：1
	console.log(myDate.getMonth()); // 打印结果：11
	console.log(myDate.getFullYear()); // 打印结果：2019
	console.log(myDate.getHours()); // 打印结果：11
	console.log(myDate.getMinutes()); // 打印结果：12
	console.log(myDate.getSeconds()); // 打印结果：30
	console.log(myDate.getMilliseconds()); // 打印结果：817

	console.log(myDate.getTime()); // 获取时间戳。打印结果：1575861150817

---

## getTime()：获取时间戳

Date对象 还有如下方法：

getTime() 获取当前日期对象的时间戳。这个方法在实际开发中，用得比较多。

> **时间戳**：指的是从格林威治标准时间的1970年1月1日，0时0分0秒到当前日期所花费的**毫秒数**（1秒 = 1000毫秒）。

计算机底层在保存时间时，使用的都是时间戳。时间戳的存在，就是为了**统一**时间的单位。

format()

将时间对象转换为指定格式。

---

# 15.内置对象 Math

## 内置对象 Math 的常见方法

|方法       | 描述           |   备注    |
| ------------- |:-------------:|-------------|
| Math.abs()     | 返回绝对值 |          |
| Math.floor()      | 向下取整（向小取）	 |        |
| Math.ceil()	 | 向上取整（向大取）  |     |
| Math.round() | 四舍五入取整（正数四舍五入，负数五舍六入）	    |     |
| Math.random() | 生成0-1之间的随机数   |   不包含0和1    |
| Math.max(x, y, z) | 返回多个数中的最大值    |       |
| Math.min(x, y, z) | 返回多个数中的最小值  |  |
| Math.pow(x,y)	 | 返回 x 的 y 次幂  |   |
| Math.sqrt() | 对一个数进行开方运算  |   |

Math 和其他的对象不同，它不是一个构造函数，不需要创建对象。
Math属于一个工具类，里面封装了数学运算相关的属性和方法。

举例：

    var num = -0.6;

    console.log(Math.abs(num));        //取绝对值

    console.log(Math.floor(num));      //向下取整，向小取

    console.log(Math.ceil(num));       //向上取整，向大取

    console.log(Math.round(num));      //四舍五入取整（正数四舍五入，负数五舍六入）

    console.log(Math.random());        //生成0-1之间的随机数

    结果打印：
    0.6
    -1
    -0
    -1
    0.8781965680308945

---

## Math.random()方法举例：生成 x-y 之间的随机数

生成 0-x 之间的随机数：

    Math.round(Math.random()*x)

生成 x-y 之间的随机数：

    Math.round(Math.random()*(y-x)+x)

---

## url 编码和解码

URI (Uniform ResourceIdentifiers,通用资源标识符)进行编码，以便发送给浏览器。有效的URI中不能包含某些字符，例如空格。而这URI编码方法就可以对URI进行编码，它们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器能够接受和理解。

    encodeURIComponent();   //把字符串作为 URI 组件进行编码
    decodeURIComponent();   //把字符串作为 URI 组件进行解码

举例：

    var url = "https://mayanming696.com";

    var str = encodeURIComponent(url);
    console.log(str);                           //打印url的编码
    console.log(decodeURIComponent(str));       //对url进行编码后，再解码，还原为url

打印结果：

![](10.png)

---

# 16.正则表达式简介

> 定义：正则表达式用于定义一些字符串的规则。
>作用：计算机可以根据正则表达式，来检查一个字符串是否符合指定的规则；或者将字符串中符合规则的内容提取出来。
如果你想查看正则更多的内容，可以查阅官方文档关于 RegExp 这个内置对象的用法。

**创建正则表达式的对象**
## 方式一：使用构造函数创建正则表达式的对象**
语法：

	var 变量 = new RegExp("正则表达式"); // 注意，参数是字符串

	var 变量 = new RegExp("正则表达式", "匹配模式"); // 注意，两个参数都是字符串

备注：RegExp的意思是 Regular expression。使用typeof检查正则对象，会返回object。

上面的语法中，既可以传一个参数，也可以传两个参数。

创建了正则表达式的对象后，该怎么使用呢？大致分为两个步骤：

* （1）创建正则表达式的对象 reg。

* （2）使用 reg 的test() 方法，判断指定字符串是否符合规则。

**正则表达式的test()方法：【重要】**

> 解释：使用test()这个方法可以用来检查一个字符串是否符合正则表达式的规则，如果符合则返回true，否则返回false。

myReg.test(str); // 判断字符串 str 是否符合 指定的 myReg 这个正则表达式的规则

**1.传一个参数**

构造函数 RegExp 中，可以只传一个参数。

代码解析：

	var reg = new RegExp("a"); // 定义一个正则表达式：检查一个字符串中是否含有 a

	var str1 = "mayanming";
	var str2 = "june";

	// 通过 test()方法，判断字符串是否符合 上面定义的 reg 规则
	console.log(reg.test(str1)); // 打印结果：true
	console.log(reg.test(str2)); // 打印结果：false

注意，上面的例子中，我们是先定义了一个正则表达式的规则，然后通过正则表达式的test()方法来判断字符串是否符合之前定义的规则。

**2.传两个参数时：匹配模式 【重要】**

构造函数 RegExp 中，也可以传两个参数。我们可以传递一个**匹配模式**作为第二个参数。这个参数可以是：
* i 忽略大小写。这里的 i 指的是 ignore。
* g 全局匹配模式。这里的 g 指的是 global。

代码举例：

    var reg = new RegExp('m', 'i');
    var str = 'mayanming';

    console.log(reg.test(str)); // 打印结果：true

---

## 方式二：使用字面量创建正则表达式

我们可以使用字面量来创建正则表达式。

语法：

	var 变量 = /正则表达式/;  // 注意，这个语法里没有引号

	var 变量 = /正则表达式/匹配模式;  // 注意，这个语法里没有引号

代码举例：

	var reg = /a/i; // 定义正则表达式的规则：检查一个字符串中是否含有 a。忽略大小写。
	var str = "mayanming";

	console.log(typeof reg);  // 打印结果：object
	console.log(reg.test(str)); // 打印结果：true

---

## 两种方式的对比

以上两种方式的对比：

* 方式一：使用构造函数创建时，更加灵活，因为参数中还可以传递变量。
* 方式二：使用字面量的方式创建，更加简单。

代码举例：

	var reg = new RegExp("a", "i"); // 方式一

	var reg = /a/i; // 方式二

**上面这两行代码的作用是等价的。**

---

## 正则表达式字符匹配攻略

**1 横向模糊匹配**

横向模糊指的是，一个正则可匹配的字符串的长度不是固定的，可以是多种情况的。
其实现的方式是使用量词。譬如{m,n}，表示连续出现最少m次，最多n次。

比如/ab{2,5}c/表示匹配这样一个字符串：第一个字符是“a”，接下来是2到5个字符“b”，最后是字符“c”。测试如下：

    var regex = /ab{2,4}c/g;

    var string = "abc abbc abbbc abbbbc abbbbbc abbbbbbc";

    console.log( string.match(regex) );

    打印结果：
    ["abbc", "abbbc", "abbbbc"]

**注意：**案例中用的正则是/ab{2,5}c/g，后面多了g，它是正则的一个修饰符。表示全局匹配，即在目标字符串中按顺序找到满足匹配模式的所有子串，**强调的是“所有”**，而不只是“第一个”。g是单词global的首字母。

**2 纵向模糊匹配**
纵向模糊指的是，一个正则匹配的字符串，具体到某一位字符时，它可以不是某个确定的字符，可以有多种可能。
其实现的方式是使用字符组。譬如[abc]，表示该字符是可以字符“a”、“b”、“c”中的任何一个。
比如/a[123]b/可以匹配如下三种字符串："a1b"、"a2b"、"a3b"。测试如下：

    var regex = /a[123]b/g;

    var string = "a0b a1b a2b a3b a4b";

    console.log( string.match(regex) );

    打印结果：
    ["a1b", "a2b", "a3b"]

---

## 2.字符组

* 2.1 范围表示法

比如 [ 123456abcdefGHIJKLM ]，可以写成[ 1-6a-fG-M ]。用连字符-来省略和简写。

因为连字符有特殊用途，那么要匹配“a”、“-”、“z”这三者中任意一个字符，该怎么做呢？

可以写成如下的方式：[ -az ]或[ az- ]或[ a\-z ] 总之不会让引擎认为是范围表示法就行了

* 2.2 排除字符组

此时就是排除字符组（反义字符组）的概念。例如[^abc]，表示是一个除"a"、"b"、"c"之外的任意一个字符。字符组的第一位放^（脱字符），表示求反的概念。

* 2.3 常见的简写形式

\d就是[ 0-9]。表示是一位数字。记忆方式：其英文是digit（数字）。

\D就是[ ^0-9]。表示除数字外的任意字符。

\w就是[ 0-9a-zA-Z_]。表示数字、大小写字母和下划线。记忆方式：w是word的简写，也称单词字符。

\W是[ ^0-9a-zA-Z_]。非单词字符。

\s是[ \t\v\n\r\f]。表示空白符，包括空格、水平制表符、垂直制表符、换行符、回车符、换页符。记忆方式：s是space character的首字母。

\S是[^ \t\v\n\r\f]。 非空白符。

.就是[ ^\n\r\u2028\u2029]。通配符，表示几乎任意字符。换行符、回车符、行分隔符和段分隔符除外。记忆方式：想想省略号...中的每个点，都可以理解成占位符，表示任何类似的东西。

## 3. 量词

{m,} 表示至少出现m次。

{m} 等价于{m,m}，表示出现m次。

? 等价于{0,1}，表示出现或者不出现。记忆方式：问号的意思表示，有吗？

/+ 等价于{1,}，表示出现至少一次。记忆方式：加号是追加的意思，得先有一个，然后才考虑追加。

/*  等价于{0,}，表示出现任意次，有可能不出现。记忆方式：看看天上的星星，可能一颗没有，可能零散有几颗，可能数也数不过来。

通过在量词后面加个问号就能实现惰性匹配

---
之后补充












    
















        
---
title: JS-原型链详解
date: 2019-10-11 12:05:45
top: false
cover: false
toc: true
mathjax: true
password:
summary: Javascript-(原型链)
tags:
- Javascript
categories:
- Javascript学习
---

# 一. 普通对象与函数对象

JavaScript 中，万物皆对象！但对象也是有区别的。分为 **普通对象**和 **函数对象**，Object 、Function 是 JS 自带的函数对象。下面举例说明

![](1.jpg)

在上面例子中 o1 o2 o3 为普通对象，f1 f2 f3为函数对象。区分的很简单，凡是通过 **new Function()创建的对象都是函数对象，其余都是普通对象，Function Object也都是通过New Function()创建的** ，f1 f2,归根结底都是通过new Function()方式进行创建。

---

# 二.构造函数

![](2.jpg)

上面例子中 person1 和 person2 都是 Person 的 **实例**， 这两个实例都有一个 constructor (构造函数) 属性，该属性(是一个指针)指向 Person 即：

![](3.jpg)

得出两个概念(构造函数，实例)：
**person1 和 person2 都是 构造函数Person 的实例**
公式：
**实例的构造函数属性(constructor)指向构造函数**

---

# 三.原型对象

在 JavaScript 中，每当定义一个对象（函数也是对象）时候，对象中都会包含一些预定义的属性。其中每个**函数对象**都有一个**prototype 属性**，这个属性指向函数的**原型对象**

![](4.jpg)

我们得到文本定律：

             每个对象都有 _proto_ 属性，但只有函数对象才有 prototype 属性

>原型对象，其实就是个普通对象，在上面我给Person.prototype 添加了4个属性： name , age ,job ,sayName,其实还有一个默认的属性：constructor
在默认情况下，所有的原型对象都会自动获得一个 constructor (构造函数)属性，这个属性(是一个指针)指向 prototype 属性所在的函数(Person)

上面这句话有点拗口，我们「翻译」一下：A 有一个默认的 constructor 属性，这个属性是一个指针，指向 Person。即：

        Person.prototype.constructor == Person

在上面第二小节《构造函数》里，我们知道实例的构造函数属性（constructor）指向构造函数 ：

        person1.constructor == Person

![](5.jpg)

person1 为什么有 constructor 属性？那是因为 person1 是 Person 的实例。
那 Person.prototype 为什么有 constructor 属性？？同理， Person.prototype （你把它想象成 A） 也是Person 的实例。
也就是在 Person 创建的时候，创建了一个它的实例对象并赋值给它的 prototype

**结论：原型对象（Person.prototype）是 构造函数（Person）的一个实例。**

原型对象其实就是普通对象（但 Function.prototype 除外，它是函数对象，但它很特殊，他没有prototype属性（前面说道函数对象都有prototype属性））。看下面的例子：

![](6.jpg)

**Function.prototype 为什么是函数对象呢？**

>上文提到凡是通过 new Function( ) 产生的对象都是函数对象。因为 A 是函数对象，所以Function.prototype 是函数对象。

那原型对象是用来做什么的呢？主要作用是用于继承。举个例子：

![](7.jpg)

故两次 this 在函数执行时都指向 person1。

---

# 四.__proto__(原型链)

JS 在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做 **__proto__** 的内置属性，**用于指向创建它的构造函数的原型对象**。
对象 person1 有一个 __proto__属性，创建它的构造函数是 Person，构造函数的原型对象是 Person.prototype ，所以：

        person1.__proto__ == Person.prototype
        (_proto_指向构造函数的原型对象)
![](8.jpg)

根据上面这个连接图，我们能得到：

        Person.prototype.constructor == Person;
        person1.__proto__ == Person.prototype;
        person1.constructor == Person;

**不过，要明确的真正重要的一点就是，这个连接存在于实例（person1）与构造函数（Person）的原型对象（Person.prototype）之间，而不是存在于实例（person1）与构造函数（Person）之间。**

---

# 五.总结

>
 * 原型和原型链是JS实现继承的一种模型。
 * 原型链的形成是真正是靠__proto__ 而非prototype
 * 对象通过__proto__属性访问原型，构造函数通过prototype属性访问原型
 * Object 是所有对象的爸爸，所有对象都可以通过 proto 找到它
 * Function 是所有函数的爸爸，所有函数都可以通过 proto 找到它
 * Function.prototype 和 Object.prototype 是两个特殊的对象，他们由引擎来创建
 * 除了以上两个特殊对象，其他对象都是通过构造器 new 出来的
 * 函数的 prototype 是一个对象，也就是原型 
   对象的_proto_指向原型， _proto_将对象和原型连接起来组成了原型链



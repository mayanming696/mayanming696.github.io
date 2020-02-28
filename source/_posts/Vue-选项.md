---
title: Vue-选项
date: 2020-02-26 14:56:46
comments: false
top: false
cover: false
password:
toc: true
mathjax: false
summary: Vue2.0基础
tags:
- Vue
categories:
- Vue学习

---

# computed 计算选项

computed 的作用主要是对原数据进行改造输出。改造输出：包括格式的编辑，大小写转换，顺序重排，添加符号……。

我们先来做个读出价格的例子：我们读书的原始数据是price:100 但是我们输出给用户的样子是（￥100元）。 主要的javascript代码：

    computed:{
        newPrice:function(){
            return this.price='￥' + this.price + '元';
        }
    }

全部代码:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>Computed Option 计算选项</title>
    </head>
    <body>
        <h1>Computed Option 计算选项</h1>
        <hr>
        <div id="app">
            {{newPrice}}
        </div>

        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                data:{
                    price:100
                },
                computed:{
                    newPrice:function(){
                        return this.price='￥' + this.price + '元';
                    }
                }
            })
        </script>
    </body>
    </html>

computed 属性是非常有用，在输出数据前可以轻松的改变数据。

---

# Methods 方法选项

我们还是复习一下最简单的使用方法，一个数字，每点击一下按钮加1.

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>methods Option</title>
    </head>
    <body>
        <h1>methods Option</h1>
        <hr>
        <div id="app">
            {{ a }}
            <p><button @click="add">add</button></p>
        </div>
        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                data:{
                    a:1
                },
                methods:{
                    add:function(){
                        this.a++
                    }
                }
            })
        </script>
    </body>
    </html>

## 1.methods中参数传递

使用方法和正常的javascript传递参数的方法一样，分为两部：

**在methods的方法中进行声明，比如我们给add方法加上一个num参数，就要写出add:function(num){}.**

**调用方法时直接传递，比如我们要传递2这个参数，我们在button上就直接可以写。
    
    <button @click=”add(2)”></button>.

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>methods Option</title>
    </head>
    <body>
        <h1>methods Option</h1>
        <hr>
        <div id="app">
            {{ a }}
            <p><button @click="add(2)">add</button></p>
        </div>

        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                data:{
                    a:1
                },
                methods:{
                    add:function(num){
                        if(num!=''){this.a+=num}
                        else{this.a++}
                    }
                }
            })
        </script>
    </body>
    </html>

## 2.methods中的 $event参数

传递的$event参数都是关于你点击鼠标的一些事件和属性。我们先看看传递的方法。

    <button @click=”add(2,$event)”>add</button> 

我们这时候可以打印一下，看看event到底是个怎样的对象。你会发现，它包含了大部分鼠标事件的属性。

## 3.native 给组件绑定构造器里的原生事件

在实际开发中经常需要把某个按钮封装成组件，然后反复使用，如何让组件调用构造器里的方法，而不是组件里的方法。就需要用到我们的.native修饰器了。

现在我们把我们的add按钮封装成组件：

声明btn对象：

    var btn:{
        template:`<buttom>组件</buttom>`
    }

在构造器里声明：

    components:{
        "btn":btn
    }

用.native修饰器来调用构造器里的add方法

    <p><btn @click.native="add(3)"></btn></p>


## 4.在作用域外调用构造器里的方法

这种不经常使用，如果你出现了这种情况，说明你的代码组织不够好。

    <button onclick="app.add(4)" >外部调用构造器里的方法</button>

---

# Watch 监控数据选项选项



## 编写一个监控变化实例

温度大于26度时，我们建议穿T恤短袖，温度小于26度大于0度时，我们建议穿夹克长裙，温度小于0度时我们建议穿棉衣羽绒服。

先来模拟一个温度变化的情况：我们使用按钮来加减温度。

1.在构造器外面方式一

    app.$watch('temperature',function(newVal,oldVal){
        if(newVal>=26){
            this.suggestion="T恤短裙";
        }else if(newVal<26 && newVal >=0)
        {
            this.suggestion="夹克外套";
        }else{
            this.suggestion="羽绒服";
        }
    })


2.在构造器里面方式二

watch:{
    wendu:function(newVal,oldVal){
         if(newVal>=26){
            this.suggestion="T恤短裙";
        }else if(newVal<26 && newVal >=0)
        {
            this.suggestion="夹克外套";
        }else{
            this.suggestion="羽绒服";
        }
}

---

# Mixins混入选项

Mixins一般有两种用途：

* 在你已经写好了构造器后，需要增加方法或者临时的活动时使用的方法，这时用混入会减少源代码的污染。
* 很多地方都会用到的公用方法，用混入的方法可以减少代码量，实现代码重用。

## 一、Mixins的基本用法

我们现在有个数字点击递增的程序，假设已经完成了，这时我们希望每次数据变化时都能够在控制台打印出提示：“数据发生变化”.

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>Mixins Option Demo</title>
    </head>
    <body>
        <h1>Mixins Option Demo</h1>
        <hr>
        <div id="app">
            <p>num:{{ num }}</p>
            <P><button @click="add">增加数量</button></P>
        </div>

        <script type="text/javascript">
            //额外临时加入时，用于显示日志
            var addLog={
                updated:function(){
                    console.log("数据放生变化,变化成"+this.num+".");
                }
            }
            var app=new Vue({
                el:'#app',
                data:{
                    num:1
                },
                methods:{
                    add:function(){
                        this.num++;
                    }
                },
                mixins:[addLog]//混入
            })
        </script>
    </body>
    </html>

## 全局API混入Mixin

我们也可以定义全局的混入，这样在需要这段代码的地方直接引入js，就可以拥有这个功能了。我们来看一下全局混入的方法：

    Vue.mixin({
        updated:function(){
            console.log('我是全局被混入的');
        }
    })

## mixins调用顺序

1.全局mixins 
2.mixins混入
3.构造器执行

当混入方法和构造器的方法重名时，混入的方法无法展现，也就是不起作用。

---

# extends 拓展

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>Extends Optin Demo</title>
    </head>
    <body>
        <h1>Extends Optin Demo</h1>
        <hr>
        <div id="app">
            {{message}}
            <p><button @click="add">add</button></p>
        </div>

        <script type="text/javascript">
            var bbb={
                created:function(){
                    console.log("我是被扩展出来的");
                },
                methods:{
                    add:function(){
                        console.log('我是被扩展出来的方法！');
                    }
                }
            };
            var app=new Vue({
                el:'#app',
                data:{
                    message:'hello Vue!'
                },
                methods:{
                    add:function(){
                        console.log('我是原生方法');
                    }
                },
                extends:bbb
            })
        </script>
    </body>
    </html>







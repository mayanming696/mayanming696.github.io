---
title: Vue-全局API
date: 2020-02-23 14:44:50
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

#  1、什么是全局API？
全局API并不在构造器里，而是先声明全局变量或者直接在Vue上定义一些新功能，Vue内置了一些全局API，比如我们今天要学习的指令Vue.directive。说的简单些就是，**在构造器外部用Vue提供给我们的API函数来定义新的功能。**

---

# 2、Vue.directive自定义指令

    Vue.directive('marco'(使用时候要v-marco),function(el,binding,vnode){
            el.style='color:'+binding.value;
        });
        var app=new Vue({
            el:'#app',0-
            data:{
                num:10,
                color:'green'
            },
            methods:{
                add:function(){
                    this.num++;
                }
            }
        })

## 1.自定义指令中传递的三个参数

* el: 指令所绑定的元素，可以用来直接操作DOM。(整个标签)
* binding: 一个对象，包含指令的很多信息。(是一个对象，很多属性)
* vnode: Vue编译生成的虚拟节点。

## 2.自定义指令的生命周期

自定义指令有五个生命周期(也叫钩子函数)，分别是 bind,inserted,update,componentUpdated,unbind

* bind:只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个绑定时执行一次的初始化动作。（绑定时候调用）
* inserted:被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于document中）。（插入时候调用）
* update:被绑定于元素所在的模板更新时调用，而无论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新。（更新时候使用）
* componentUpdated:被绑定元素所在模板完成一次更新周期时调用。（完成时使用）
* unbind:只调用一次，指令与元素解绑时调用。
    unbind 解绑的函数：
    function unbind(){
        app.$destory();
    }

---

# 3、Vue的生命周期函数(钩子函数)

Vue一共有10个生命周期函数，我们可以利用这些函数在vue的每个阶段都进行操作数据或者改变内容。

    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>构造器的声明周期</title>
    </head>
    <body>
    <h1>构造器的声明周期</h1>
    <hr>
    <div id="app">
        {{message}}
        <p><button @click="jia">加分</button></p>
    </div>
        <button onclick="app.$destroy()">销毁</button>
    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:1
            },
            methods:{
                jia:function(){
                    this.message ++;
                }
            },
            beforeCreate:function(){
                console.log('1-beforeCreate 初始化之后');
            },
            created:function(){
                console.log('2-created 创建完成');
            },
            beforeMount:function(){
                console.log('3-beforeMount 挂载之前');
            },
            mounted:function(){
                console.log('4-mounted 被创建');
            },
            beforeUpdate:function(){
                console.log('5-beforeUpdate 数据更新前');
            },
            updated:function(){
                console.log('6-updated 被更新后');
            },
            activated:function(){
                console.log('7-activated');
            },
            deactivated:function(){
                console.log('8-deactivated');
            },
            beforeDestroy:function(){
                console.log('9-beforeDestroy 销毁之前');
            },
            destroyed:function(){
                console.log('10-destroyed 销毁之后')
            }
        })
        </script>
    </body>
    </html>

---

# 4、Tempalate制作模板

##  一、直接写在选项里(构造器里)的模板

直接在构造器里的template选项后边编写。这种写法比较直观，但是如果模板html代码太多，不建议这么写。

javascript代码：

    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        },
        template:`
            <h1 style="color:red">我是选项模板</h1>
        `
    })

在选项template里面写HTML就行
这里需要注意的是模板的标识不是单引号和双引号，而是，就是Tab上面的键。

##  二、写在tempalte标签里的模板

这种写法更像是在写HTML代码，就算不会写Vue的人，也可以制作页面。

    <template id="demo2">
             <h2 style="color:red">我是template标签模板</h2>
    </template>
    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },
            template:'#demo2'
        })
    </script>

---

##  三、写在script标签里的模板

这种写模板的方法，可以让模板文件从外部引入。

    <script type="x-template" id="demo3">
        <h2 style="color:red">我是script标签模板</h2>
        (可以在这外部引用)
    </script>

    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },
            template:'#demo3'
        })
    </script>

以后学习到vue-cli的时候还会学到一种xxx.vue的写法。

---

# 5、Component初识组件

组件就是制作自定义的标签，这些标签在HTML中是没有的

##  一、全局化注册组件

全局化就是在构造器的外部用Vue.component来注册，我们注册现在就注册一个的组件来体验一下。

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>component-1</title>
    </head>
    <body>
        <h1>component-1</h1>
        <hr>
        <div id="app">
            <marco></marco>
        </div>
        <script type="text/javascript">
            //注册全局组件
            Vue.component('marco',{
                template:`<div style="color:red;">全局化注册的marco标签</div>`
            })
            var app=new Vue({
                el:'#app',
                data:{
                }
            })
        </script>
    </body>
    </html>

我们在javascript里注册了只能注册一个组件，在HTML中调用了他。这就是最简单的一个组件的编写方法，并且它可以放到多个**构造器的作用域**里。

## 二、局部注册组件

局部注册组件局部注册组件和全局注册组件是向对应的，局部注册的组件只能在组件注册的作用域里进行使用，其他作用域使用无效。

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>component-1</title>
    </head>
    <body>
        <h1>component-1</h1>
        <hr>
        <div id="app">
        <panda></panda>
        </div>
        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                components:{
                    "panda":{
                        template:`<div style="color:red;">局部注册的panda标签</div>`
                    }
                }
            })
        </script>
    </body>
    </html>

从代码中你可以看出局部注册其实就是写在构造器里，但是你需要注意的是，构造器里的components 是加s的，而全局注册是不加s的

## 三、组件和指令的区别

**组件注册的是一个标签，而指令注册的是已有标签里的一个属性。**在实际开发中我们还是用组件比较多，指令用的比较少。因为指令看起来封装的没那么好，这只是个人观点

---

# 6、Component 组件的 props 属性设置

props选项就是设置和获取标签上的属性值的，例如我们有一个自定义的组件,这时我们想给他加个标签属性写成 意思就是熊猫来自中国，当然这里的China可以换成任何值。定义属性的选项是props。

## 一、定义属性并获取属性值

定义属性我们需要用props选项，加上数组形式的属性名称，例如：props:**[ ‘ here ’ ]**。在组件的模板里读出属性值只需要用插值的形式，例如{{ here }}.

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>component-2</title>
    </head>
    <body>
        <h1>component-2</h1>
        <hr>
        <div id="app">
        <panda here="China"></panda>
        </div>

        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                components:{
                    "panda":{
                        template:`<div style="color:red;">Panda from {{ here }}.</div>`,
                        props:['here']
                    }
                }
            })
        </script>
    </body>
    </html>

上面的代码定义了panda的组件，并用props设置了here的属性值，在here属性值里传递了China给组件。 最后输出的结果是红色字体的Panda from China.

## 二、在构造器里向组件中传值

把构造器中data的值传递给组件，我们只要进行绑定就可以了。v-bind:xxx.


    <panda v-bind:here="message"></panda>
    var app=new Vue({
                el:'#app',
                data:{
                message:'SiChuan' 
                },
                components:{
                    "panda":{
                        template:`<div style="color:red;">Panda from {{ here }}.</div>`,
                        props:['here']
                    }
                }
            })

---

# 7、Component 父子组件关系

在实际开发中我们经常会遇到在一个自定义组件中要使用其他自定义组件，这就需要一个父子组件关系。

## 一、构造器外部写局部注册组件

上面我们都把局部组件的编写放到了构造器内部，如果组件代码量很大，会影响构造器的可读性，造成拖拉和错误。

我们把组件编写的代码放到构造器外部或者说单独文件。

我们需要先声明一个对象,对象里就是组件的内容。

    var marcoo = {
    template:`<div>Panda from China!</div>`
    }

声明好对象后在构造器里引用就可以了。

    components:{
        "marco":marcoo
    }

html中引用

    <marco></marco>

## 二、父子组件的嵌套 我们先声明一个父组件，比如叫jspang，然后里边我们加入一个city组件，我们来看这样的代码如何写。

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>component-3</title>
    </head>
    <body>
        <h1>component-3</h1>
        <hr>
        <div id="app">
        <jspang></jspang>  
        </div>
        <script type="text/javascript">
        var city={
            template:`<div>Sichuan of China</div>`
        }
            var jspang = {
                template:`<div>
                        <p> Panda from China!</p>
                        <city></city>
                </div>`,
                components:{
                    "city":city
                }
            }
            var app=new Vue({
                el:'#app',
                components:{
                    "jspang":jspang
                }
            })
        </script>
    </body>
    </html>

---

# 8、Component标签(Vue自带)

标签是Vue框架自定义的标签，它的用途就是可以动态绑定我们的组件，根据数据的不同更换不同的组件。

1.我们先在构造器外部定义三个不同的组件，分别是componentA,componentB和componentC.

    var componentA={
        template:`<div>I'm componentA</div>`
    }
    var componentB={
        template:`<div>I'm componentB</div>`
    }
    var componentC={
        template:`<div>I'm componentC</div>`
    }

2.我们在构造器的components选项里加入这三个组件。

    components:{
        "componentA":componentA,
        "componentB":componentB,
        "componentC":componentC,
    }

3.我们在html里插入component标签，并绑定who数据，根据who的值不同，调用不同的组件。

    <component v-bind:is="who"></component>

这就是我们的组件标签的基本用法。我们提高以下，给页面加个按钮，每点以下更换一个组件。

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>component-4</title>
    </head>
    <body>
        <h1>component-4</h1>
        <hr>
        <div id="app">
        <component v-bind:is="who"></component>
        <button @click="changeComponent">changeComponent</button>
        </div>
        <script type="text/javascript">
            var componentA={
                template:`<div style="color:red;">I'm componentA</div>`
            }
            var componentB={
                template:`<div style="color:green;">I'm componentB</div>`
            }
            var componentC={
                template:`<div style="color:pink;">I'm componentC</div>`
            }
            var app=new Vue({
                el:'#app',
                data:{
                    who:'componentA'
                },
                components:{
                    "componentA":componentA,
                    "componentB":componentB,
                    "componentC":componentC,
                },
                methods:{
                    changeComponent:function(){
                        if(this.who=='componentA'){
                            this.who='componentB';
                        }else if(this.who=='componentB'){
                            this.who='componentC';
                        }else{
                            this.who='componentA';
                        }
                    }
                }
            })
        </script>
    </body>
    </html>

---
---
title: Vue-内部指令
date: 2019-10-10 10:09:12
comments: false
top: false
cover: false
password:
toc: true
mathjax: false
summary:  Vue-内部指令的解析
tags:
- Vue
categories:
- Vue学习
---


# 一、v-if的使用：

* v-if:是vue 的一个内部指令，指令用在我们的html中。
* v-if用来判断是否加载html的DOM，比如我们模拟一个用户登录状态，在用户登录后现实用户名称。

        <div v-if="isLogin">你好，Marco！</div>

 **完整html代码:**

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <script type="text/javascript" src="../assets/js/vue.js"></script>
            <title>v-if & v-show & v-else</title>
        </head>
        <body>
            <h1>v-if 判断是否加载</h1>
            <hr>
            <div id="app">
                <div v-if="isLogin">你好：Marco</div>
                <div v-else>请登录后操作</div>
            </div>
            <script type="text/javascript">
                var app=new Vue({
                    el:'#app',
                    data:{
                    isLogin:false
                    }
                })
            </script>
        </body>
        </html>

这里我们在vue的data里定义了isLogin的值，当它为true时，网页就会显示：你好：Marco，如果为false时，就显示请登录后操作。

---

# 二、v-show的使用：

调整css中display属性，DOM已经加载，只是CSS控制没有显示出来。

    <div v-show="isLogin">你好：JSPang</div>

**v-if 和v-show的区别:**
* v-if： 判断是否加载，可以减轻服务器的压力，在需要时加载。
* v-show：调整css dispaly属性，可以使客户端操作更加流畅。

# 三、v-for指令 ：解决模板循环问题

v-for指令是循环渲染一组data中的数组，v-for 指令需要以 item in items 形式的特殊语法，items 是源数据数组并且item是数组元素迭代的别名。

## 1、基本用法：
 
 模板写法

    <li v-for="item in items">
            {{item}}
    </li>

 js写法

    var app=new Vue({
        el:'#app',
        data:{
            items:[20,23,18,65,32,19,54,56,41]
        }
    })

 完整代码：

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>V-for 案例</title>
    </head>
    <body>
        <h1>v-for指令用法</h1>
        <hr>
        <div id="app">
        <ul>
            <li v-for="item in items">
                    {{item}}
            </li>
        </ul>
        </div>
    
        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                data:{
                    items:[20,23,18,65,32,19,54,56,41]
                }
            })
        </script>
    </body>
    </html>

 这是一个最基础的循环，先在js里定义了items数组，然后在模板中用v-for循环出来，需要注意的是，你需要那个html标签循环，v-for就写在那个上边。

 ## 2、排序

 我们已经顺利的输出了我们定义的数组，但是我需要在输出之前给数组排个序，那我们就用到了Vue的computed:属性。

        computed:{
            sortItems:function(){
                return this.items.sort();
            }
        }

我们在computed里新声明了一个对象sortItems，如果不重新声明会污染原来的数据源，这是Vue不允许的，所以你要重新声明一个对象。

如果一切顺利的话，你已经看到了结果，但是这个小程序还是有个小Bug的，现在我把数组修改成这样。

        items:[20,23,18,65,32,19,5,56,41]

我们把其中的54修改成了5，我们再看一下结果，发现排序结果并不是我们想要的。

我们可以自己编写一个方法sortNumber，然后传给我们的sort函数解决这个Bug。

        function sortNumber(a,b){
                    return a-b
        }

用法

        computed:{
            sortItems:function(){
            return this.items.sort(sortNumber);
            }
        }

经过一番折腾，我们终于实现了真正的数字排序，这是在工作中非常常用的，一定要学好，记住。

## 三、对象循环输出

我们上边循环的都是数组，那我们来看一个对象类型的循环是如何输出的。

我们先定义个数组，数组里边是对象数据

    students:[
    {name:'jspang',age:32},
    {name:'Panda',age:30},
    {name:'PanPaN',age:21},
    {name:'King',age:45}
    ]

在模板中输出

    <ul>
    <li v-for="student in students">
        {{student.name}} - {{student.age}}
    </li>
    </ul>

加入索引序号：

    //数组对象方法排序:
    function sortByKey(array,key){
        return array.sort(function(a,b){
        var x=a[key];
        var y=b[key];
        return ((x<y)?-1:((x>y)?1:0));
    });
    }

有了数组的排序方法，在computed中进行调用排序

    sortStudent:function(){
        return sortByKey(this.students,'age');
    }

注意：vue低版本中 data里面的items和computed里面可以一样，但是高版本，是不允许相同名称。有很多小伙伴踩到了这个坑，这里提醒学习的小伙伴，根据自己版本的不同，请修改代码。

---

# 四、v-text & v-html

我们已经会在html中输出data中的值了，我们已经用的是,这种情况是有弊端的，就是当我们网速很慢或者javascript出错时，会暴露我们的。Vue给我们提供的v-text,就是解决这个问题的。我们来看代码： 

    <span>{{ message }}</span>=<span v-text="message"></span><br/>

如果在javascript中写有html标签，用v-text是输出不出来的，这时候我们就需要用v-html标签了。

    <span v-html="msgHtml"></span>

双大括号会将数据解释为纯文本，而非HTML。为了输出真正的HTML，你就需要使用v-html 指令。 需要注意的是：在生产环境中动态渲染HTML是非常危险的，因为容易导致XSS攻击。所以只能在可信的内容上使用v-html，永远不要在用户提交和可操作的网页上使用。 完整代码：

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>v-text & v-html 案例</title>
    </head>
    <body>
        <h1>v-text & v-html 案例</h1>
        <hr>
        <div id="app">
            <span>{{ message }}</span>=<span v-text="message"></span><br/>
            <span v-html="msgHtml"></span>
        </div>
    
        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                data:{
                    message:'hello Vue!',
                    msgHtml:'<h2>hello Vue!</h2>'
                }
            })
        </script>
    </body>
    </html>

---

# 五、v-on：绑定事件监听器

v-on 就是监听事件，可以用v-on指令监听DOM事件来触发一些javascript代码。

一、使用绑定事件监听器，编写一个加分减分的程序。

程序代码

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <script type="text/javascript" src="../assets/js/vue.js"></script>
        <title>v-on事件监听器</title>
    </head>
    <body>
        <h1>v-on 事件监听器</h1>
        <hr>
        <div id="app">
        本场比赛得分： {{count}}<br/>
        <button v-on:click="jiafen">加分</button>
        <button v-on:click="jianfen">减分</button>
    
        </div>
    
        <script type="text/javascript">
            var app=new Vue({
                el:'#app',
                data:{
                    count:1
                },
                methods:{
                    jiafen:function(){
                        this.count++;
                    },
                    jianfen:function(){
                        this.count--;
                    }
                }
            })
        </script>
    </body>
    </html>

我们的v-on 还有一种简单的写法，就是用@代替。

    <button @click="jianfen">减分</button>

我们除了绑定click之外，我们还可以绑定其它事件，比如键盘回车事件v-on:keyup.enter,现在我们增加一个输入框，然后绑定回车事件，回车后把文本框里的值加到我们的count上。 绑定事件写法：

    <input type="text" v-on:keyup.enter="onEnter" v-model="secondCount">

javascript代码：

    onEnter:function(){
        this.count=this.count+parseInt(this.secondCount);
    }

因为文本框的数字会默认转变成字符串，所以我们需要用parseInt()函数进行整数转换。

你也可以根据键值表来定义键盘事件： 

---

# 六、v-model指令

v-model指令，我理解为绑定数据源。就是把数据绑定在特定的表单元素上，可以很容易的实现双向数据绑定。

## 1、最简单的双向数据绑定代码：

html文件

    <div id="app">
        <p>原始文本信息：{{message}}</p>
        <h3>文本框</h3>
        <p>v-model:<input type="text" v-model="message"></p>
    </div>

javascript代码：

    var app=new Vue({
    el:'#app',
    data:{
        message:'hello Vue!'
    }
    })

## 2、修饰符

* .lazy：取代 imput 监听 change 事件。
* .number：输入字符串转为数字。
* .trim：输入去掉首尾空格。

## 3、文本区域加入数据绑定

    <textarea  < cols="30" rows="10" v-model="message"></textarea>

## 4、多选按钮绑定一个值

    <h3>多选按钮绑定一个值</h3>
    <input type="checkbox" id="isTrue" v-model="isTrue">
    <label for='isTrue'>{{isTrue}}</label>

## 5、多选绑定一个数组
  
    <h3>多选绑定一个数组</h3>
        <p>
                <input type="checkbox" id="JSPang" value="JSPang" v-model="web_Names">
                <label for="JSPang">JSPang</label><br/>
                <input type="checkbox" id="Panda" value="Panda" v-model="web_Names">
                <label for="JSPang">Panda</label><br/>
                <input type="checkbox" id="PanPan" value="PanPan" v-model="web_Names">
                <label for="JSPang">PanPan</label>
                <p>{{web_Names}}</p>
    </p>

## 6、单选按钮绑定数据

    <h3>单选按钮绑定</h3>
    <input type="radio" id="one" value="男" v-model="sex">
    <label for="one">男</label>
    <input type="radio" id="two" value="女" v-model="sex">
    <label for="one">女</label>
    <p>{{sex}}</p>

---

# 七、v-bind 指令

v-bind是处理HTML中的标签属性的

html文件：

    <div id="app">
        <img v-bind:src="imgSrc"  width="200px">
    </div>

在html中我们用v-bind:src=”imgSrc”的动态绑定了src的值，这个值是在vue构造器里的data属性中找到的。

js文件：

    var app=new Vue({
        el:'#app',
        data:{
            imgSrc:'http://baidu.com/wp-content/uploads/2017/02/vue01-2.jpg'
        }
    })

我们在data对象在中增加了imgSrc属性来供html调用

**v-bind 缩写**

    <!-- 完整语法 -->
    <a v-bind:href="url"></a>
    <!-- 缩写 -->
    <a :href="url"></a>

**绑定CSS样式**

* 1.在工作中我们经常使用v-bind来绑定css样式：

在绑定CSS样式是，绑定的值必须在vue中的data属性中进行声明。 1、直接绑定class样式

        <div :class="className">1、绑定classA</div>

* 2.绑定classA并进行判断，在isOK为true时显示样式，在isOk为false时不显示样式。

        <div :class="{classA:isOk}">2、绑定class中的判断</div>

* 3.绑定class中的数组

        <div :class="[classA,classB]">3、绑定class中的数组</div>

* 4.绑定class中使用三元表达式判断

        <div :class="isOk?classA:classB">4、绑定class中的三元表达式判断</div>

* 5.绑定style

        <div :style="{color:red,fontSize:font}">5、绑定style</div>   

* 6.用对象绑定style样式

        <div :style="styleObject">6、用对象绑定style样式</div>

        var app=new Vue({
        el:'#app',
        data:{
            styleObject:{
                fontSize:'24px',
                color:'green'
                    }
                }
        })        

---




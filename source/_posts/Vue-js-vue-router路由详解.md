---
title: Vue-router路由详解
date: {{ date }}
comments: false
top: false
cover: false
password:
toc: true
mathjax: false
summary: Vue路由详情
tags:
- Vue
categories:
- Vue学习

---
>*基本介绍*
---
# **什么是 vue-router?**
 (1)***vue-router*** 是Vue官方提供前端路由插件包，借助它我们实现可以基于路由和组件的单页面应用，路径管理器
 (2)它与传统的页面区别在于：
* 传统的页面应用采用的是后端路由，即通过超链接来实现页面切换和跳转的。
* 而在 ***vue-router*** 单页面应用中，则是通过路径之间的切换（实际上就是组件的切换）。

---
# **安装配置**
 (1)如果我们使用 ***vue-cli*** 脚手架来搭建项目，在开始配置过程会选择是否需要安装路由，具体参考我之前的这篇文章：
 * [Vue.js - 使用vue-cli搭建项目（附：详细操作步骤）](/2019/09/07/vue-quan-jia-tong/)
  
(2)如果项目搭建时没有安装也没关系，可以执行如下命令手动安装：

    npm install vue-router


---
>**路由分类**

# 1.router-link 制作导航
* router-link 是一个组件，它默认会被渲染成一个带有链接的a标签，通过to属性指定链接地址,当然也可以使用 v-bind 来动态设置
* 使用 *** <router-link>***，在 HTML5 的 History 模式下会拦截点击，避免浏览器重新加载页面。
* 注意：被选中的router-link将自动添加一个class属性值 ***.router-link-active***
   
        <router-link to="/">[text]</router-link>
* 除了 to 属性外，<router-link> 还有一些其他常用的 prop：
 * **tag** 可以指定渲染成什么标签。比如下面渲染的结果就是 ***li*** 而不是 ***a***

        <router-link to="/hello" tag="li">跳转到 hello</router-link>
 * **replace** 配置后不会留下 History 记录，即导航后不能用后退键返回上一个页面。

        <router-link to="/hello" replace>跳转到 hello</router-link>
 * active-class
    * 当 <router-link> 对应的路由匹配成功时，会自动给当前元素设置一个名为 router-link-active 的 class。我们通常会利用它来高亮显示当前页面对应的导航菜单项。
    * 而通过设置 active-class 可以修改默认的 class 样式名称（router-link-active），不过一般情况下我们也不需要改它，使用默认就好了。                   
* to：导航路径，要填写的是你在router/index.js文件里配置的path值，
如果要导航到默认首页，只需要写成 to="/" ，
* [text] ：就是我们要显示给用户的导航名称。
---
# 2.router-view 用于渲染匹配到的组件
会根据当前路由动态渲染不同的页面组件
用Vue-cli脚手架创建了项目结构，***src文件目录下会有一个router文件夹***,编写路由组件的地方在
 ***编写路由组件的地方***
***路由的核心文件:src/router/index.js*** 
 ***运行网页时，<router-view> 会根据当前路由动态渲染不同的页面组件***
 ***而页面中的其它部分（比如本样例顶部的图片）的内容，在路由切换时，是不会发生变化的***
 >下面是核心文件解析

![](1.jpg)

---
# 3.vue-router配置子路由（嵌套路由、二级路由）
在Hi页面的下面新建两个子页面，分别是 “Hi页面1” 和 “Hi页面2”，来实现子路由。
把Hi.vue改成一个通用(母版)的模板，加入 ***<router-view>***标签，给子模板提供插入位置。“Hi页面1” 和 “Hi页面2” 都相当于“Hi页面”的子页面，有点想继承关系。我们在“Hi页面”里加入 ***<router-view>***标签。
***然后路由配置如图***


![](2.png)

---
# 4.使用 JS 代码进行跳转
除了使用 ***<router-link>*** 进行跳转外，我们也可以借助如下几个方法在 JavaScript 里进行页面跳转。
*  **1，this.$router.push()**

        <template>
        <div>
            <h1>首页</h1>
            <a @click="handleRouter">跳转到 hello</a>
        </div>
        </template>
        
        <script>
        export default {
        methods: {
            handleRouter() {
            this.$router.push("/hello");
            }
        }
        }
        </script>

* **2，this.$router.replace()**
该方法则类似于 <router-link> 的 replace 功能，它不会向 history 添加新记录，而是替换掉当前的 history 记录。

        this.$router.replace("/hello");

* **3，this.$router.go()**
该方法类似与 **window.history.go()**，在 history 记录中向前或者后退多少步，参数是整数。

        //后退1页
        this.$router.go(-1);
        
        //前进2页
        this.$router.go(2);




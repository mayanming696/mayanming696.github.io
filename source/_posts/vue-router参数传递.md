---
title: Vue-router参数传递
date: 2019-09-10 16:03:11
comments: false
top: false
cover: false
password:
toc: true
mathjax: false
summary: Vue-router参数传递
tags:
- Vue
categories:
- Vue学习
---

# **一、使用冒号（:）的形式传递参数(URL传递参数)**

>**1，路由列表的参数设置**

（1）路由列表的 path 是可以带参数的，我们在路由配置文件（router/index.js）里以冒号的形式设置参数。
（2）下面样例代码中，我在跳转到欢迎页面（/hello）时，带有两个参数 : **id** 和 **userName**。

![](1.png)

>**2，参数的传递**

（1）如果使用 <router-link> 组件跳转的话，可以这么携带参数：

	
        <router-link to="/hello/123/hangge">跳转到 hello</router-link>
（2）如果使用 js 代码跳转的话，可以这么携带参数：


        this.$router.push("/hello/123/hangge");

>**3，参数的获取**

页面中通过 $route.params.xxx 获取传递过来的数据。

        <template>
    <div>
        <h1>ID：{{ $route.params.id}}</h1>
        <h1>用户名：{{ $route.params.userName}}</h1>
    </div>
    </template>

>**4，运行效果**

可以看到点击首页链接进行跳转后，参数成功传递并显示。


---

# **二、使用 query 方式传递参数(to传递，参数显示URL)**

>**1，路由列表**

query 方式类似 get 传参，即通过 URL 传递参数。而路由列表的 path 不需要配置参数：

![](2.png)

>**2，参数的传递**

（1）如果使用 <router-link> 组件跳转的话，可以这么携带参数：

        <router-link :to="{path:'/hello', query:{id:123, userName:'hangge'}}">
        跳转到 hello
        </router-link>

（2）如果使用 js 代码跳转的话，可以这么携带参数：

        this.$router.push({
        path:'/hello',
        query:{id:123, userName:'hangge'}
        });

>**3，参数的获取**

页面中通过 $route.query.xxx 获取传递过来的数据。

        <template>
        <div>
            <h1>ID：{{ $route.query.id}}</h1>
            <h1>用户名：{{ $route.query.userName}}</h1>
        </div>
        </template>

>**4，运行效果**

可以看到点击首页链接进行跳转后，参数是自动拼接到 url 后面进行传递的。


---

# **三、使用 params 方式传递参数(to传递，参数不显示URL 推荐)**

>**1，路由列表**

params 方式类似于 post 传参，即传递的参数不会显示在 URL 上。同上面的 query 方式一样，路由列表的 path 不需要配置参数：

![](3.png)

>**2，参数的传递**

 **注意：params 只能用 name 来引入路由，而不能用 path。**
 （1）如果使用 <router-link> 组件跳转的话，可以这么携带参数：

        <router-link :to="{name:'hello', params:{id:123, userName:'hangge'}}">
        跳转到 hello
        </router-link>

（2）如果使用 js 代码跳转的话，可以这么携带参数：

        this.$router.push({
        name:'hello',
        params:{id:123, userName:'hangge'}
        });

>**3，参数的获取**

页面中通过 $route.params.xxx 获取传递过来的数据。

        <template>
        <div>
            <h1>ID：{{ $route.params.id}}</h1>
            <h1>用户名：{{ $route.params.userName}}</h1>
        </div>
        </template>

>**4，运行效果**

可以看到这种方式，参数的传递不会拼接到 url 后面。

---

# 附：使用 props 实现参数解耦 

 从上面的样例可以看出，当路由携带参数跳转时，页面这边通过 ***$route.params.xxx*** 或 ***$route.query.xxx*** 来获取传递过来的数据。但这样有个问题，由于组件中使用 $route 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。
    要解决这个问题，我们可以使用 props 将组件和路由解耦。props 共有如下三种模式。

>**1，布尔模式**

（1）直接将路由配置中的 props 属性被设置为 true，那么参数将会被设置为组件属性。

![](4.png)

（2）然后我们页面组件这边不再需要通过 $route.params.xxx 或 $route.query.xxx 来获取传递过来的数据。


![](5.png)

>**2，对象模式**

（1）我们可以将 props 设置为一个对象，对象内容会被设置为组件属性。这种方式常用来配置静态参数。


![](6.png)

（2）然后页面组件这边获取数据方式和前面一样。


![](7.png)

>**3，函数模式**

（1）我们还可以创建一个函数返回 props，在函数中对参数值进行处理，或者将静态值与基于路由的值结合。


![](8.png)

（2）这里假设我们使用 JS 进行跳转，代码如下：


![](9.png)

（3）目标页面组件代码，以及运行结果如下：

![](10.png)



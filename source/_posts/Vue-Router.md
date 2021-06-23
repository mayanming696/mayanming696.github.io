---
title: Vue-Router
date: 2021-06-23 15:44:54
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/Vue-Router.png'
summary: Vue路由
cover: true
tags:
- Vue
---

Vue 路由的代码解析
<!-- more -->

## Vue router 安装

其实 {% span red, Vue router %}是一个{% span red, Vue %}项目的插件，基本都是会使用他所以就必备项目搭配脚手架npm安装如果安装较慢或者失败就换成国内镜像(cnpm)。

``` bash
npm install vue-router --save-dev
```

## 解析 router 文件

我们使用Vue全家桶后,自动生成了项目默认目录基础等,{% span red, src/router/index.js %} 文件，这就是我们路由的核心文件了。如下：


``` bash
import Vue from 'vue'   //引入Vue
import Router from 'vue-router'  //引入vue-router
import Index from '@/src/view/Index'  //引入根目录下的Hello.vue组件

Vue.use(Router)  //Vue全局使用Router

export default new Router({
  routes: [              //配置路由，这里是个数组
    {                    //每一个链接都是一个对象,默认首页是第一个
      path: '/',         //链接路径
      name: 'Index',     //路由名称，
      component: Index   //对应的组件模板
    }
  ]
})
```

## 使用 router 跳转

我们在{% span red, src/view %}目录下,新建我们{% span red, Second.vue %}文件，相当于创建我们的首页内容

``` bash
<template>
  <div class="secondWarp">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'second',
  data () {
    return {
      msg: '这是第二个页面进行跳转'
    }
  }
}
</script>


<style scoped>

</style>
``` 

然后我们需要引入新组件:我们首先在{% span red, router/index.js %}文件上注册引入挂载新组件

``` bash
import Vue from 'vue'   //引入Vue
import Router from 'vue-router'  //引入vue-router
import Index from '@/src/view/Index'  //引入根目录下的Hello.vue组件
import Second from '@/src/view/Second' 

Vue.use(Router)  //Vue全局使用Router

export default new Router({
  routes: [              //配置路由，这里是个数组
    {                    //每一个链接都是一个对象
      path: '/',         //链接路径
      name: 'Index',     //路由名称，
      component: Index   //对应的组件模板
    },{
      path:'/second',
      name:'Second',
      component:Second
    }
  ]
})
```

在方法中调用

``` bash
this.$router.push('second') //在需要的调用方法这样便可以跳转新页面

//<router-link>标签调用类似于HTML <a> 标签,<router-view>为展示路由内容
   <router-link to="/">跳转首页</router-link>
   <router-link to="/second">跳转第二个页面</router-link>
```

这里写着发现自己会混淆 组件调用跟路由跳转的概念，我的理解是组件是包含父组件中于子组件中存在数据的传递，路由的改变是直接URL的变化是无法进行父组件的的数据交互，独立的行为因为他会让该路由初始化状态。否则项目大了不好管理。

## 配置子路由

子路由的情况一般用在一个页面有他的基础模版，然后它下面的页面都隶属于这个模版，只是部分改变样式。

``` bash
import Vue from 'vue'   
import Router from 'vue-router'  
import Index from '@/src/view/Index'  
import Second from '@/src/view/Second' 
import Second1 from '@/src/view/Second1' 
import Second2 from '@/src/view/Second2' 

Vue.use(Router) 

export default new Router({
  routes: [             
    {                    
      path: '/',        
      name: 'Index',     
      component: Index   
    },{
      path:'/Second',
      component:Second,
      //单子路由
      children:[
        {path:'/',component:Second,left:Second1,right:Second2},
        {path:'second1',component:Second1},
        {path:'second2',component:Second2}, //name 可以用于一个父页面多个子页面的精准分配
      ]
      //多子路由同页面展示
      compontents:{
　　　　　right:second2,
         left:second1
　　　　}
    }
  ]
})
```

想实现多个router-view就要使用components，并在里面配置router-view的name属性对应的组件。default是默认路由，就是不设置路由的router-view都会显示default指向的组件。
将此钉子 {% span red, router-view %}埋于他路径的上一级模板内即可
在配置路由文件前，需要先用import引入你所需要的路由文件


## 路由配置文件钩子函数

查看随意一个例子：

``` bash
{
      path:'/params/:newsId(\\d+)/:newsTitle',
      component:Params,
      beforeEnter:(to,from,next)=>{
        console.log('我进入了params模板');
        console.log(to);
        console.log(from);
        next();
},
```

to:路由将要跳转的路径信息，信息是包含在对像里边的。
from:路径跳转前的路径信息，也是一个对象的形式。
next:路由的控制参数，常用的有next(true)和next(false)。

在配置文件中的钩子函数，只有一个钩子-beforeEnter，如果我们写在实际内容页面中就可以有两个钩子函数可以使用

``` bash
export default {
  name: 'params',
  data () {
    return {
      msg: 'params page'
    }
  },
  beforeRouteEnter:(to,from,next)=>{
    console.log("准备进入路由模板");
    next();
  },
  beforeRouteLeave: (to, from, next) => {
    console.log("准备离开路由模板");
    next();
  }
}
</script>
```

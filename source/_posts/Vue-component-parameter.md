---
title: Vue 父子组件之间传值
date: 2021-01-13 10:46:14
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/component.png'
summary: Vue提升
cover: true
tags:
- Vue
---

Vue 父组件与子组件之间的参数传递解析
<!-- more -->

## Vue 父组件=>子组件（动态传值)

遇到问题前提uni-app框架，项目需要父组件接口获取数据后(动态)传值并调用子组件，一直都是空值，甚至打印长度为0，数据却显示长度不为0。

## 方法一：
props传值，传过来的值需要用watch监听并更新，否则为{% span red, 空值 %}
原因数据还没有被赋值的时候，子组件就已经显示在页面上了

``` bash
父组件（template）
 <shmily-drag-image :list="dataImgList"></shmily-drag-image>

父组件 （script）
this.dataImgList=res.data.imgList; //参数赋值
``` 

这里把接口返回的数组赋值给
this.dataImgList，然后把该数组传给子组件定义的props属性list

``` bash
子组件（props）
   props: {
    list: {
      type: Array,
      default: function() {
        return []
      }
    }
   }
子组件 (watch：监听数据变化)
watch:{
    list(newVal,oldVal){
     if(newVal){
       this.sonImgList=curVal;
      }
   },
}
``` 

此方法数据 this.list 数据进行父组件子组件绑定

## 方法二：
通过ref属性，父组件调用子组件的方法，把要传的数组作为参数传给子组件，子组件获取该参数，并使用

``` bash
父组件（template）
<shmily-drag-image ref="fatherImgList"  :list="dataImgList" ></shmily-drag-image>
父组件 （script）
this.$refs.fatherImgList.getSrcList(this.dataImgList); 
``` 

``` bash
子组件（script）
	getSrcList(val){
        this.sonImgList=val;
	},
``` 

子组件向父组件传值，如果是动态改变的，也要记得加{% span red, watch %}函数，动态改变之后执行的操作写在watch里，比如 {% span red, this.$emit %}的函数！




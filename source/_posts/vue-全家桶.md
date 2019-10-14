---
title: Vue 全家桶
date: {{ date }}
comments: false
top: false
cover: false
password:
toc: true
mathjax: false
summary: Vue全家桶搭建
tags:
- Vue
categories:
- Vue学习
---
# 搭建项目架构,**技术胖大神**  
---
# **Vue本地搭建**
# **安装 npm**
环境安装
***可以在命令行工具里输入***

>***npm -v***

*   检测和查询版本
* 下载地址 ：***http://nodejs.cn/download/***

* 用 npm命令来安装Vue-cli
  Vue-cli是脚手架工具，作用是用配置好的模板迅速搭建一个项目工程，省去Webpack默认打包配置规则

***在命令行输入下面命令***

> ***npm install vue-cli -g***

  * -g 代表全局安装

---  
# **安装 vue**
>***vue -V***

 * 用来检测安装版本以及是否安装成功

---
# **初始化项目**
>***$ vue init webpack 项目名称***

(init :初始化项目)

 * Project name：项目名称（直接回车则使用括号中默认名字）
 * Project description：项目描述（直接点击回车则使用默认名字）
 * Author：作者 (如果你有配置git的作者，他会读取。)
 * Runtime + Compiler: recommended for most users：运行加编译
 * Runtime-only：仅运行时
 * Install vue-router?：是否安装 vue-route（这是官方的路由，大多数情况下都使用 Y）
 * Use ESLint to lint your code?：是否使用 ESLint 管理代码（ESLint 是个代码风格管理工具，是用来统一代码风格的，一般项目中都会使用。)
 * Pick an ESLint preset：选择一个 ESLint 预设，编写 vue 项目时的代码风格
 * Setup unit tests with Karma + Mocha?：是否安装单元测试 N
 * Setup e2e tests with Nightwatch?：是否安装 e2e 测试 N
  
>**cd 项目名称**

  进入我们的vue项目目录

  
>**npm install**

NPM通常称为node包管理器，主要功能就是管理node包，包括：安装、卸载、更新、查看、搜索、发布等。NPM是基于couchdb一个数据库，详细记录了每个包的信息（作者、版本、依赖、授权信息等）
 * 安装我们的项目依赖包，也就是安装package.json里的包
 * 1.允许用户从 npm 服务器下载别人编写的第三方包到本地使用。
 * 2.允许用户从 npm 服务器下载并安装别人编写的命令行程序到本地使用。
 * 3.允许用户将自己编写的包或命令行程序上传到 npm 服务器供别人使用。  

---
# **运行项目**
>**npm run dev**

  开发模式下运行我们的程序。给我们自动构建了开发用的服务器环境和在浏览器中打开，并实时监视我们的代码更改，即时呈现给我们。

---
# **打包发布项目**
>**npm run build**

 * 在项目开发完成之后，我们可以执行如下命令来进行打包工作。
 * 打包完成后，项目中会生成 ***dist*** 文件夹，我们只需要 ***dist*** 文件夹里的内容放到服务器上就行了。


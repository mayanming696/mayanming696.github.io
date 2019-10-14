---
title: Hexo博客 +GitHub 搭建与关联
date: {{ date }}
comments: false
top: true
cover: false
password:
toc: 
mathjax: true
summary: Hexo搭建
tags:
- Hexo
categories:
- Hexo学习
---

<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=407679465&auto=1&height=66"></iframe></div>


# 搭建Hexo博客 - Github 

>搭建Hexo博客 - Github 大体流程：
* 1.Hexo本地搭建
* 2.Github 搭建
* 3.Hexo关联Github 并且通过本地上线到Github
* 4.域名与 github 绑定 
   
---
**1.Hexo 本地搭建**，**韦阳大神**
---
**环境安装**
***安装 Node.js ***
***检验是否安装成功 ***
>+ **Win + R**

    node -v

    npm -v

 出现序列号就是安装成功
*** 安装 Git ***
 输入自己的项目名字，后面加入 *.github.io* 后缀，然后README 初始化也勾选上，名称一定要和前面的github名字完全一样
*** 在设置里面选择主题 ***

**安装Hexo**
---
* **本地合适的地方新建一个文件夹**
在该目录右键点击 ***Git Bash Here*** ,打开git的控制窗口，就不用再windows 自带的运行窗口进行了
* **定位到该目录下** 安装Hexo
出现报错无视

    npm i hexo-cli -g

安装完成后输入

    hexo -v

 检测是否安装完成初始化hexo 文件
输入

    hexo init

初始化文件夹 ，然后安装 

    npm install

安装必备的组件,完成检测
输入

    hexo g

生成静态文件 
输入

    hexo s

  打开本地服务器，出现 ***http://localhost:4000/*** 则完成安装
关闭本地服务器 

>***ctrl +c *** 

---
# 2.连接Github与本地

对着目标文件夹右键 ***git bash***,然后输入下面命令

    git config --global user.name "你的GitHub用户名"

    git config --global user.email "你的GitHub注册邮箱"


  生成密匙SSH key

    ssh-keygen -t rsa -C "注册邮箱"

  一直默认回车 在git bash

    cat ~/.ssh/id_rsa.pub 

  将输出内容处置到Github 账号设置里面的SSH key

    ssh -T git@github.com

  在git bash 输入出现你的用户名等信息就是成功了
  在博客根目录的 **_config.yml** 文件配置信息  
    
 --- 
# 3.本地上传文章，发布文章

首先在博客根目录右键打开 ***git bash*** ,
安装一个拓展 

    ***npm i hexo-deployer-git***

***然后输入*** 
  
    hexo new post "名称"

新建一篇文章 ***\blog\source\_posts***的目录，可以发现下面多了一个文件夹和一个 ***.md***文件，一个用来存放你的图片等数据，另一个就是你的文章文件啦,编写完文件后，根目录下

***输入*** 

    hexo g
  
生成静态网页，然后
***输入*** 

    hexo s
  
 可以本地预览效果，最后
 ***输入***
   
    hexo d
   
 上传到github上。这时打开你的github.io主页就能看到发布的文章啦
  
---
# 4.域名绑定
//

> 我遇见谁，会有怎样的对白。
我等的人，她在多远的未来。


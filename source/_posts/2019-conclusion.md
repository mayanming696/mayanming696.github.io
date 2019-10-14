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

![](5.jpg)

然后我进行了国内外分流的，Coding 跟 github 一样的操作

---
# 5.源码备份 

## 备份操作

使用Hexo在github搭建的博客，博客作为一个单独的GitHub仓库存在，但是这个仓库只有生成的静态网页文件，并没有Hexo的源文件，如果要换电脑或者重装系统后，就比较麻烦了，这里推荐一种方法。

1. 创建两个分支：master和hexo

2. 设置hexo为默认分支；

3. 将刚刚创建的新仓库clone至本地，将之前的hexo文件夹中的_config.yml，themes/，source/，scaffolds/，package.json，.Username.github.io文件夹

4. 将themes/matery/(我用的是matery主题)中的.git/删除，否则无法将主题文件夹push；

5. 在Username.github.io文件夹执行npm install和npm install hexo-deployer-git（这里可以看一看分支是不是显示为hexo）；

6. 执行git add .、git commit -m ""、git push origin hexo来提交hexo网站 **源文件**；

7. 执行hexo g -d生成静态网页部署至Github上。

这样做法，Username.github.io仓库就有master 和 hexo 分支，分别保存静态网页跟源文件

## 修改操作

再本地对博客修改（修改主题样式，发布新文章等操作）后：

1. 依次执行

        git add .
        git commit -m ""
        git push origin hexo

    来提交源文件；


2. 执行 

        hexo g
        hexo d

生成静态网页并且部署到Github上

重复6-7的步骤

## 恢复

重装电脑，或者再其他电脑上修改博客的时候
1. 安装git
2. 安装Nodejs 和npm
3. 使用 git clone git@github.com:mayanming696/mayanming696.github.io.git 将仓库拷至本地；
4. 再文件夹内执行下面命令

        npm install hexo-cli -g
        npm install
        npm install hexo-deployer-git

最后重新添加SSH

最后附注HEXO的源文件 备份操作的步骤4，只需拷贝6个，而不需要全部：

    1 ._config.yml站点的配置文件，需要拷贝
    2 .themes/主题文件夹，需要拷贝；
    3 .source博客文章的.md文件，需要拷贝；
    4 .scaffolds/文章的模板，需要拷贝；
    5 .package.json安装包的名称，需要拷贝；
    6 .gitignore限定在push时哪些文件可以忽略，需要拷贝；
    7 .git/主题和站点都有，标志这是一个git项目，不需要拷贝；
    8 node_modules/是安装包的目录，在执行npm install的时候会重新生成，不需要拷贝；
    9 public是hexo g生成的静态网页，不需要拷贝；
    10 .deploy_git同上，hexo g也会生成，不需要拷贝；
    11 db.json文件，不需要拷贝。
其实不需要拷贝的文件正是.gitignore中所忽略的。 





> 我遇见谁，会有怎样的对白。
我等的人，她在多远的未来。


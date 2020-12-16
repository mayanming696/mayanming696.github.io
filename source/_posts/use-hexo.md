---
title: Hexo博客搭建
date: 2019-9-01 14:39:05
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/hexo-logo.svg'
summary: Hexo博客搭建
cover: true
tags:
- Hexo
---

从零开始开始搭建属于自己的Hexo个人博客
<!-- more -->

## 搭建Hexo博客 - Github

搭建Hexo博客 - Github 大体流程：
- 环境安装检测
- 开始搭建Hexo
- 本地项目连接Github
- 本地上传文章，发布文章
- 源码备份
- 新电脑恢复数据

## 环境安装检测

``` bash
node -v
```

``` bash
npm -v
```

各自出现序列号说明环境已安装完成
并且安装：{% span red, Git %}
{% link Git官网安装, https://git-scm.com/downloads %}

## 开始搭建Hexo

本地合适的地方新建一个文件夹
在该目录右键点击 {% span red, Git Bash Here %},打开git的控制窗口，就不用再windows 自带的运行窗口进行了

``` bash
npm i hexo-cli -g
```

安装hexo基础模块

``` bash
hexo -v

hexo init

npm install

hexo g

hexos
```

打开本地服务器，出现 http://localhost:4000/ 则完成安装

## 本地项目连接Github

1.对着目标文件夹右键 {% span red, git bash %},然后输入下面命令

``` bash
git config --global user.name "你的GitHub用户名"

git config --global user.email "你的GitHub注册邮箱"
```

2.生成密匙SSH key

``` bash
ssh-keygen -t rsa -C "注册邮箱"
```

3.一直默认回车 然后{% span red, git bash %}

``` bash
cat ~/.ssh/id_rsa.pub 
```

4.将输出内容处置到Github 账号设置里面的SSH key

``` bash
ssh -T git@github.com
```
5.在git bash 输入出现你的用户名等信息就是成功了
6.在博客 {% span green, 根目录 %} {% span red, _config.yml %} 文件配置信息

## 本地上传文章，发布文章

生成文章文件，以及基础配置

``` bash
hexo new post "名称"
```

上传到github上

``` bash
hexo clean
hexo g
hexo d
```

## 源码备份

使用Hexo在github搭建的博客，博客作为一个单独的GitHub仓库存在，但是这个仓库只有生成的静态网页文件，并没有Hexo的源文件，如果要换电脑或者重装系统后，就比较麻烦了，这里推荐一种方法。

1.创建两个分支：master和hexo
2.github上设置hexo为默认分支；
3.在Username.github.io文件夹执行npm install和npm install hexo-deployer-git（这里可以看一看分支是不是显示为hexo）
4.执行 {% span red,git add . %} 、 {% span red,git commit -m “这次提交的描述” %} 、{% span red,git push origin hexo %}来提交hexo网站 源文件；
5.执行hexo g -d生成静态网页部署至Github上。

这样做法，github仓库就有master 和 hexo 分支，分别保存静态网页跟源文件

## 新电脑恢复数据

使用 git clone 你的github静态部署文件hexo 将仓库拷至本地；

``` bash
npm install hexo-cli -g
npm install
npm install hexo-deployer-git
```

最后重新添加SSH

``` bash
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
```

其实不需要拷贝的文件正是 {% span red,.gitignore%} 文件中所忽略的。





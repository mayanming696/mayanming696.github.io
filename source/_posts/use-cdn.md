---
title: 使用jsDelivr 开源公共 CDN
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/logo-horizontal.svg'
date: 2020-12-12 11:34:59
summary: 使用开源公共 CDN
cover: true
tags:
- CDN
---

记录使用开源公共CDN，通过Github+jsDelivr 将资源CDN加速

<!-- more -->

## 新建Github仓库

![新建githun仓库](new-Github.jpg)

## 连接Github仓库

在本地目录右键 Git Bash Here，执行以下命令：

``` bash
git clone 你的CDN仓库地址
``` 

## 上传你所需要加速资源

复制需要上传的资源到本地git仓库 {% span blue, （注：jsDelivr不支持加载超过20M的资源） %}，
在本地存放需加速资源git仓库目录下右键 Git Bash Here，执行以下命令：

``` bash
git status //查看状态
git add .  //添加所有文件到暂存区
git commit -m '提交的描述'   //把文件提交到仓库
git push   //推送至远程仓库
``` 

## 发布仓库
在github 你的CDN加速仓库里面的项目里面点击 {% span red, Releases %} 发布
- 进入可设置版本号

## 使用jsDelivr引用资源

使用方法 {% span red,https://cdn.jsdelivr.net/gh/你的用户名/你的仓库名@发布的版本号/文件路径 %} 

注意：版本号不是必需的，是为了区分新旧资源，如果不使用版本号，将会直接引用最新资源，除此之外还可以使用某个范围内的版本，查看所有资源等，具体使用方法如下：

``` bash
https://cdn.jsdelivr.net/gh/user/repo@version/file // 加载任何Github发布、提交或分支
https://cdn.jsdelivr.net/gh/jquery/jquery@3.2/dist/jquery.min.js // 使用版本范围而不是特定版本
https://cdn.jsdelivr.net/gh/jquery/jquery@3/dist/jquery.min.js  // 使用版本范围而不是特定版本
https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js // 完全省略该版本以获取最新版本
``` 
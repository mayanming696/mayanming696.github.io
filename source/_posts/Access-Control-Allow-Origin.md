---
title: '解决项目跨域问题(uni-app,Vue)'
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/Access-Control-Allow-Origin.png'
date: 2021-05-17 13:32:50
summary: 跨域,Vue
cover: true
tags:
- Vue
---

{% note success, uni-app 使用H5页面请求时,出现跨域问题。%}

<!-- more -->

## 背景
- HBuilderX 3.1.13
- 使用H5时候链接测试服的API地址后出现跨域
- 切换成IP后台接口成功
- 为了方便进行配置跨域代理

## Uni-app

打开项目根目录下的 {% span red, manifest.json %}的源码视图

![manifest.json](step1.jpg)

## manifest.json文件配置
在manifest.json中编辑H5节点（没有可以手动添加此节点）：

``` bash
 "h5" : {
        "devServer" : {
			"port" : 8080,
			"https" : false,
            "disableHostCheck" : true,
			"proxy" : {
				"/api" :{
					"target" : "http://text.com:8086",
                    "changeOrigin" : true,
                    "secure" : false
					// "pathRewrite" : {
					// 	"^/api" : "/"
					// }
				}
			}
        }
 }
```

## 使用

例子接口地址：http://mayanming.com/api/shopCode

``` bash
			   uni.request({
			   	url: '/api/shopCode/',
			   	method:'POST',
			   	success(res) {
                    console.log('调用成功')
			   	},
			   	fail() {
                    console.log('异常状态')
			   	}
			   })
```

## 配置说明

manifest.json文件中配置的proxy信息为如下时：

``` bash
        "devServer" : {
			"port" : 8080,//对应你本地项目运行的端口
			"https" : false,//启用 https 协议
            "disableHostCheck" : true,//禁用 Host 检查
			"proxy" : {
				"/api" :{
					"target" : "http://text.com:8086",
                    "changeOrigin" : true,
                    "secure" : false
				}
			}
        }
```

此配置表示所有 {% span red, /api %} 开头的接口都会自动拼接上 {% span red, http://text.com:8086 %}。例如上面的例子就会变成 {% span red, http://text.com:8086/api/shopCode/ %}

不过经常我们的接口没有相似的前缀来区分，此时就需要pathRewrite来对path重写。

``` bash
 "h5" : {
        "devServer" : {
			"port" : 8080,
			"https" : false,
            "disableHostCheck" : true,
			"proxy" : {
				"/api" :{
					"target" : "http://text.com:8086",
                    "changeOrigin" : true,
                    "secure" : false
					 "pathRewrite" : {
						"^/api" : ""
					}
				}
			}
        }
 }
```

 这样的话用上面例子的请求就会变成 {% span red, http://text.com:8086/shopCode/ %} 具体需要变成怎么样则看真实项目来重写修改。

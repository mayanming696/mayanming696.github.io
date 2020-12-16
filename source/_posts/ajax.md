---
title: Ajax基础详解
headimg: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/image/heandimgbb.png'
date: 2019-9-27 14:39:05
summary: Ajax详解
cover: true
tags:
- Ajax
---

{% note success, 客户端与服务器，可以在【不必刷新整个浏览器】的情况下，与服务器进行异步通讯的技术Ajax的核心是js对象：XMLHttpRequest。 %}

<!-- more -->

## 什么是Ajax

- {% span red, 同步 %}: {% span blue, 客户端发起请求–等待–>服务器端处理—等待–>响应–>页面载入 %} 请求错误时全部重新载入.
- - 同步例子（在银行排队时，只有等到你了，才能够去处理-业务。）
- {% span red, 异步 %}: {% span blue, 客户端发起请求—>服务器端处理—>响应—>页面载入填写时 %} 即时更新,部分返回.
- - 异步例子 （在排队的时候，可以玩手机。）

{% folding cyan open, 发送 Ajax 请求的五个步骤 %}

``` bash
1.创建异步对象。即 XMLHttpRequest 对象。
2.使用open方法设置请求的参数。openmethod,url,async。参数解释：请求的方法、请求的url、是否异步。
3.发送请求。
4.注册事件。 注册onreadystatechange事件，状态改变时就会调用。如果要在数据完整请求回来的时候才调用，
我们需要手动写一些判断的逻辑。
5.获取返回的数据。
```

{% endfolding %}

## XMLHttpRequest

要创建XMLHttpRequest对象是要分两种情况考虑的：

- 在IE6以下的版本
- 在IE6以上的版本以及其他内核的浏览器Mozilla等

``` bash
 <script type="text/javascript">
    var httpRequest;
        if(window.XMLHttpRequest) {
            //在IE6以上的版本以及其他内核的浏览器(Mozilla)等
            httpRequest = new XMLHttpRequest();
        }else if(window.ActiveXObject) {
            //在IE6以下的版本
            httpRequest = new ActiveXObject();
        }
</script>
```

{% folding cyan , 了解XMLHttpRequest对象的方法 %}

1.open(String method,String url,boolean asynch,String username,String password)
2.sendcontent
3.setRequestHeaderStringheader,Stringvalue
4.getAllResponseHeaders
5.getResponseHeaderStringheader
6.abort

{% endfolding %}

解析XMLHttpRequest对象的方法的常用类：
open：该方法创建http请求
- 1.第一个参数是指定提交方式post、get
- 2.第二个参数是指定要提交的地址是哪
- 3.第三个参数是指定是异步还是同步true表示异步，false表示同步
- 4.第四个参数获取所有的响应报头,http认证的时候会用到,是可选的
- 5.第五个参数查询响应中的某个字段的值参数在http认证的时候会用到,是可选的

setRequestHeaderStringheader,Stringvalue：设置消息头（使用post方式才会使用到，get方法并不需要调用该方法）
- xmlhttp.setRequestHeader“Content−type”,”application/x−www−form−urlencoded”;

sendcontent：发送请求给服务器
- 如果是get方式，并不需要填写参数，或填写null
- 如果是post方式，把要提交的参数写上去


{% folding cyan , 了解XMLHttpRequest对象的属性 %}

1.onreadystatechange：
- 请求状态改变的事件触发器（readyState变化时会调用此方法）,一般用于指定回调函数(通过监听onreadystatechange事件,来判断请求的状态.)

{% folding cyan  yellow, 2.readyState %}
readyState：请求状态readyState一改变，回调函数被调用，它有5个状态
- 0：未初始化还没有调用open(方法)
- 1：open方法成功调用以后已调用send(方法,正在发送请求)
- 2：载入完成,服务器已经应答客户端的请求send(方法完成,已经收到全部响应 内容)
- 3：交互中解析。Http头信息已经接收，响应数据尚未接收。正在解析响应内容
- 4：完成。数据接收完成响应内容解析完成,可以在客户端调用了
{% endfolding %}

{% endfolding %}

基本完整的一个Ajax请求

``` bash
var request = new XMLHttpRequest();
request.open("GET","get.json",true); 
request.onreadystatechange = function () { 
    if (request.readyState === 4) { 
        if (request.status === 200) { 
            //响应成功,做一些事情 
            } else {
                 //响应失败,做一些事情 
                 } 
    } 
};
```

{% folding cyan open , ajax响应流程图 %}
![Ajax流程示意图](ajax响应流程图.png)
- 1.responseText：服务器返回的文本内容
- 2.responseXML：服务器返回的兼容DOM的XML内容
- 3.status：服务器返回的状态码
- 4.statusText：服务器返回状态码的文本信息
{% endfolding %}

{% folding cyan open , ajax响应流程图 %}
![Ajax返回的内容](Ajax返回的内容.png)

回调函数就是接收 {% span red, 服务器返回的内容 %}

{% endfolding %}

## 编写第一个Ajax程序

html代码
- 创建的div只要用于显示服务器返回的数据
- 当用户点击按钮的时候，就触发事件。

``` bash
    <input type="text" id="username">
    <input type="button" onclick="checkUsername()" value="检测用户名是否合法">
    <div id="result">
    </div>
``` 

JavaScript代码

``` bash
<script type="text/javascript">
    var httpRequest;
    function checkUsername() {
        if(window.XMLHttpRequest) {
            //在IE6以上的版本以及其他内核的浏览器(Mozilla)等
            httpRequest = new XMLHttpRequest();
        }else if(window.ActiveXObject) {
             //在IE6以下的版本
            httpRequest = new ActiveXObject();
        }
        //创建http请求
        httpRequest.open("POST", "Servlet1", true);
        //因为我使用的是post方式，所以需要设置消息头
        httpRequest.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
        //指定回调函数
        httpRequest.onreadystatechange = responseOk;
        //得到文本框的数据
        var name = document.getElementById("username").value;
        //发送http请求，把要检测的用户名传递进去
        httpRequest.send("username=" + name);
    }
    function responseOk() {
         //判断请求状态码是否是4【数据接收完成】
          if(httpRequest.readyState==4) {
            //再判断状态码是否为200【200是成功的】
            if(httpRequest.status==200) {
                //得到服务端返回的文本数据
                var text = httpRequest.responseText;
                //把服务端返回的数据写在div上
                var div = document.getElementById("result");
                div.innerText = text;
            }
          }
    }
``` 

## XMLHttpRequest解决缓存问题

在传统的Web中我们也解决过缓存的问题，通过设置response的头信息，返回给浏览器就可以实现不缓存页面了。
但是呢，现在我们使用XMLHttpRequest，拿到的不是全新的页面，仅仅是服务器端发送过来的数据！！
那我们要怎么解决缓存的问题呢？？产生缓存的原因就是：我们请求了同一个地址，做了相同的操作。服务端认为我的操作并没有什么变化，就直接把缓存的信息给我了。这样的话，我就不能更换验证码图片了等等应用。{% span red, 添加时间戳即可解决 %}


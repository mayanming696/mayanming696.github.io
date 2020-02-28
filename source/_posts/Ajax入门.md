---
title: Ajax入门
top: false
cover: false
toc: true
mathjax: true
date: 2019-09-27 16:31:40
password:
summary: Javascript-(Ajax)
tags:
- Javascript
categories:
- Javascript学习
---


# **什么是Ajax**

>客户端与服务器，可以在【不必刷新整个浏览器】的情况下，与服务器进行异步通讯的技术(Ajax 的核心是 js 对象：XMLHttpRequest。)

* 无刷新数据读取
    * 用户注册/在线聊天室
    * 理解同步和异步(基本都用异步请求).

        **同步: 客户端发起请求--等待-->服务器端处理---等待-->响应-->页面载入 (请求错误时全部重新载入).**
        同步例子（在银行排队时，只有等到你了，才能够去处理业务。）

        **异步: 客户端发起请求--->服务器端处理--->响应--->页面载入(填写时,即时更新,部分返回).**
        异步例子 （在排队的时候，可以玩手机。）

## 发送 Ajax 请求的五个步骤
>1.创建异步对象。即 XMLHttpRequest 对象。
2.使用open方法设置请求的参数。open(method, url, async)。参数解释：请求的方法、请求的url、是否异步。
3.发送请求。
4.注册事件。 注册onreadystatechange事件，状态改变时就会调用。
如果要在数据完整请求回来的时候才调用，我们需要手动写一些判断的逻辑。
5.获取返回的数据。

---
# **XMLHttpRequest**

>XMLHttpRequest对象是Ajax中最重要的一个对象。使用Ajax更多的是编写客户端代码，而不是服务端的代码。

## 1.创建XMLHttpRequest对象

要创建XMLHttpRequest对象是要分两种情况考虑的：
* 在IE6以下的版本
* 在IE6以上的版本以及其他内核的浏览器(Mozilla)等


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

## 2.了解XMLHttpRequest对象的属性和方法

### **方法**
1.**open()(String method,String url,boolean asynch,**String username,String password)
2.**send(content)**
3.**setRequestHeader(String header,String value)**
4.getAllResponseHeaders() 
5.getResponseHeader(String header)
6.abort()

**常用的方法就是黑色粗体的前三个**
* **open()：该方法创建http请求**
    + **第一个参数是指定提交方式(post、get)**
    + **第二个参数是指定要提交的地址是哪**
    + **第三个参数是指定是异步还是同步(true表示异步，false表示同步)**
    + 第四(获取所有的响应报头,http认证的时候会用到,是可选的)
    + 第五(查询响应中的某个字段的值参数在http认证的时候会用到,是可选的)

* **setRequestHeader(String header,String value)：设置消息头（使用post方式才会使用到，get方法并不需要调用该方法）**
    + **xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");**

* **send(content)：发送请求给服务器**
    + **如果是get方式，并不需要填写参数，或填写null**
    + **如果是post方式，把要提交的参数写上去**

### 属性
* **onreadystatechange：请求状态改变的事件触发器（readyState变化时会调用此方法）,一般用于指定回调函数**

    > 通过监听onreadystatechange事件,来判断请求的状态.

* **readyState：请求状态readyState一改变，回调函数被调用，它有5个状态**
        
    > readyState属性:响应返回所处状态

    + 0：未初始化(还没有调用open()方法)
    + 1：open方法成功调用以后(已调用send()方法,正在发送请求)
    + 2：载入完成,服务器已经应答客户端的请求(send()方法完成,已经收到全部响应 内容)
    + 3：交互中(解析)。Http头信息已经接收，响应数据尚未接收。(正在解析响应内容)
    + **4：完成。数据接收完成**(响应内容解析完成,可以在客户端调用了)


    //基本完整的一个Ajax请求
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


![](1.png)

* **responseText：服务器返回的文本内容**
* **responseXML：服务器返回的兼容DOM的XML内容**
* **status：服务器返回的状态码**
* statusText：服务器返回状态码的文本信息

回调函数就是**接收服务器返回的内容！**

![](2.png)


---
# 编写第一个Ajax程序

## html代码
* 创建的div只要用于显示服务器返回的数据
* 当用户点击按钮的时候，就触发事件。


        <input type="text" id="username">
        <input type="button" onclick="checkUsername()" value="检测用户名是否合法">
        <div id="result">
        
        </div>

## JavaScript代码
* 创建XMLHttpRequest对象
* 创建http请求
* 把文本框的数据发送给http请求的目标
* 指定回调函数
* 编写回调函数
* 发送http请求
* 回调函数得到http返回的内容，把内容写在div上



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
                httpRequest.onreadystatechange = response22;

                //得到文本框的数据
                var name = document.getElementById("username").value;

                //发送http请求，把要检测的用户名传递进去
                httpRequest.send("username=" + name);

            }

            function response22() {

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
        </script>


## 效果

# **XMLHttpRequest解决缓存问题**
在传统的Web中我们也解决过缓存的问题，通过设置response的头信息，返回给浏览器就可以实现不缓存页面了。

但是呢，现在我们使用XMLHttpRequest，拿到的不是全新的页面，仅仅是服务器端发送过来的数据！！

那我们要怎么解决缓存的问题呢？？产生缓存的原因就是：我们请求了同一个地址，做了相同的操作。服务端认为我的操作并没有什么变化，就直接把缓存的信息给我了。这样的话，我就不能更换验证码图片了(等等应用)。

我们可以这样做：

* **在每次请求url中加入一个时间戳参数【每次url就不一样了】**
* 加入时间戳参数到url时，也分两种情况
 + **url本身就带有参数了，也就是说有"?"号了，那么添加时间戳的时候就需要用"&"号**
 + [x] url没有参数，直接使用"?"号来添加时间戳


        if(url.indexOf("?") >= 0){
        url = url + "&t=" + (new Date()).valueOf();
        } else{
        url = url + "?t=" + (new Date()).valueOf();
        }

# XMLHttpRequest跨域访问
**使用XMLHttpRequest去跨域访问是会出现错误的。**
我们要怎么解决呢？？这时候就要用代理思想了
* **XMLHttpRequest先把请求提交给同域的Servlet处理**
* **同域Servlet再将XMLHttpRequest的请求提交给跨域的服务器**
* **同域Servlet得到跨域服务器的返回值，再返回给XMLHttpRequest**

这个时候，**XMLHttpRequest跨域访问就分两种(GET和POST)情况了，因为这两种提交数据的方式是不一样的！**

## 浏览器代码
* 我们需要在调用open方法之前判断一下要连接的地址是不是以http开头的，如果是则认为要访问的是跨域的资源
* 首先将当前url中的”?”变成”&”，这是因为将要连接的地址改为”Proxy?url=” + url以后，如果原来url地址中有参数的话，新的url地址中就会有两个“?”这会导致服务器端解析参数错误，”url=”之后的内容表示本来要访问的跨域资源的地址。

## GET方式

GET方式是直接把参数的信息都放在url地址上，所以处理起来会相对简单。

步骤：

* 使用StringBuilder装载着getParameter("url")【获取得到地址，呆会要做拼接，所以用StringBuilder】
* **得到其他参数的时候，做URLEncode.encode()，因为我们进入Servlet的时候已经被decode了一次【我们要尽可能保留原始请求】(参照解决中文乱码) **
* 遍历所有的请求参数，只要名字不是"url"，就添加到StringBuilder中【第一个参数为"?",其他的参数为"&"】(http://localhost:8080/url?aa=bb&cc=dd)
* 创建URL对象，把拼接成的StringBuilder传递进去
* 使用BufferReader读取远程服务器返回的数据，要指定输入流编码格式，否则会乱码


            BufferedReader reader = new BufferedReader(new InputStreamReader(URL对象.openSteam(),"UTF-8"));

* 最后，把远程服务器读取到的数据再返回给XMLHttpRequest

## POST方式

POST方式把参数的信息都封装到HTTP请求中，在URL进行连接的时候，需要把数据写给远程服务器

步骤：

* 得到url参数，创建StringBuilder
* **得到其他参数的时候，做URLEncode.encode()，因为我们进入Servlet的时候已经被decode了一次【我们要尽可能保留原始请求】(参照解决中文乱码) **
* 遍历所有的请求参数，只要名字不是"url"，就添加到StringBuilder中【第一个参数直接给出,其他的参数为"&"】(aa=bb&cc=dd&ee=ff)
* 创建URL对象，创建URL连接器，允许写数据到远程服务器上


        URL url = new URL(url);
        URLConnection connection = url.openConnection;
        connection.setDoOutPut(true);

* 得到写数据流


    OutputSteamWriter writer = new OutputSteamWriter(conncetion.getOutputSteam)

* 把StringBuilder的数据写到远程服务器上，并flush
* 使用BufferReader读取远程服务器返回的数据


	BufferedReader reader =  new BufferedReader(new InputSteamReader(conncetion.inputSteamReader,"UTF-8"));
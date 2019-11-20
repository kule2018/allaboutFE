## TCP/IP协议分层管理

![img](https://img2018.cnblogs.com/blog/1330623/201811/1330623-20181111094517799-658969358.png)



## 三次握手和四次挥手

三次握手：
第一次握手：client将标志位SYN置为1，随机产生一个值为seq=J，并将该数据包发送给server,client进入SYN_SENT状态，等待server确认。
第二次握手：server收到数据包后由标志位SYN=1知道client请求建立连接，server将标志位SYN和ACK都置为1，ack=J+1，随机产生一个值seq=K，并将数据包发送给client以确认连接请求，server进入SYN_RCVD状态。
第三次握手：client收到确认后，检查ack是否为J+1，ACK是否为1，如果正确将标志位置为1，并将该数据包发送给server,server检查ACK是否为1，如果正确则连接建立成功，client和server就可以建立连接。

SYN=1  seq=J

SYN=ACK=1  ack=J+1 seq=K

四次挥手;
第一次挥手：client发送一个FIN，用来关闭client到server的数据传送，client进入FIN_WAIT_1状态。
第二次挥手：server收到FIN后，发送一个ACK给client，确认序号为收到序号+1，server进入CLOSE_WAIT状态。
第三次挥手：server发送一个FIN，用来关闭server到client的数据传送，server进入LAST_ACK状态。
第四次挥手：client收到FIN后，client进入TIME_WAIT状态，接着发送一个ACK给server,确认序号为收到序号+1，server进入CLOSED状态，完成第四次挥手。

#### 为什么挥手四次？

在建立连接的时候,Server把响应客户端的请求和请求客户端的确认放在一起发送给客户端了,即第二次握手时有SYN+ACK

而断开连接的时候,一个方向的断开,只是说明该方向数据已传输完毕,而另一个方向或许还有数据,所以得等到另一个方向数据也全部传输完成后,才能执行第三次挥手



## HTTP方法

根据 HTTP 标准，HTTP 请求可以使用多种请求方法。

HTTP1.0 定义了三种请求方法： GET, POST 和 HEAD方法。

HTTP1.1 新增了六种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。

| 序号 | 方法    | 描述                                                         |
| :--- | :------ | :----------------------------------------------------------- |
| 1    | GET     | 请求指定的页面信息，并返回实体主体。                         |
| 2    | HEAD    | 类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头 |
| 3    | POST    | 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改。 |
| 4    | PUT     | 从客户端向服务器传送的数据取代指定的文档的内容。             |
| 5    | DELETE  | 请求服务器删除指定的页面。                                   |
| 6    | CONNECT | HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。    |
| 7    | OPTIONS | 允许客户端查看服务器的性能。                                 |
| 8    | TRACE   | 回显服务器收到的请求，主要用于测试或诊断。                   |
| 9    | PATCH   | 是对 PUT 方法的补充，用来对已知资源进行局部更新 。           |



## get和Post区别

![img](https://pics3.baidu.com/feed/1b4c510fd9f9d72ab60c3af13e6e5830359bbbbf.jpeg?token=2d144f5a8eaffc33e6a662d162698007&s=E190E1331F1C55C8465D6CDA0100E0B3)



## HTTP建立持久连接的意义

HTTP/1.1 允许 HTTP 设备在事务处理结束之后将 TCP 连接保持在打开状态，以便为未来的 HTTP 请求重用现存的连接。在事务处理结束后仍然保持在打开状态的 TCP 连接被称为持久连接。

不建立持久连接，每次发送Http请求都会消耗很多的额外资源，即连接的建立与销毁。







## 存储机制localStorage、sessionStorage与Cookie存储技术

![img](https://uploadfiles.nowcoder.com/images/20170724/4363819_1500879601483_918630CC01D938FDA4587A29DA149C9F)



## cookie和session

session和cookie的作用有点类似，都是为了存储用户相关的信息。不同的是，cookie是存储在本地浏览器，而session存储在服务器。存储在服务器的数据会更加的安全，不容易被窃取。但存储在服务器也有一定的弊端，就是会占用服务器的资源，但现在服务器已经发展至今，一些session信息还是绰绰有余的



## TCP与UDP区别

**小结TCP与UDP的区别：**

1.基于连接与无连接；
2.对系统资源的要求（TCP较多，UDP少）；
3.UDP程序结构较简单；
4.流模式与数据报模式 ；

5.TCP保证数据正确性，UDP可能丢包，TCP保证数据顺序，UDP不保证。

 

```
tcp协议和udp协议的差别     TCP           UDP 
是否连接                  面向连接     面向非连接 
传输可靠性                 可靠        不可靠 
应用场合                  少量数据    传输大量数据 
速度                         慢         快
```



## XSS攻击及防御

**XSS攻击全称跨站脚本攻击，是为不和层叠样式表(Cascading Style Sheets, CSS)的缩写混淆，故将跨站脚本攻击缩写为XSS，XSS是一种在web应用中的计算机安全漏洞，它允许恶意web用户将代码植入到提供给其它用户使用的页面中。从而达到攻击的目的。如，盗取用户Cookie、破坏页面结构、重定向到其它网站等。**

XSS攻击防御

设置HttpOnly以避免cookie劫持的危险。

过滤，对诸如

<>、<img>、<a>

等标签进行过滤。

编码，像一些常见的符号，如<>在输入的时候要对其进行转换编码，这样做浏览器是不会对该标签进行解释执行的，同时也不影响显示效果。

限制，通过以上的案例我们不难发现xss攻击要能达成往往需要较长的字符串，因此对于一些可以预期的输入可以通过限制长度强制截断来进行防御。



## WEB攻击

- [XSS](https://www.cnblogs.com/morethink/p/8734103.html#XSS)

- [SQL注入](https://www.cnblogs.com/morethink/p/8734103.html#SQL注入)

  攻击者成功的向服务器提交恶意的SQL查询代码，程序在接收后错误的将攻击者的输入作为查询语句的一部分执行，导致原始的查询逻辑被改变，额外的执行了攻击者精心构造的恶意代码。

- [DDOS](https://www.cnblogs.com/morethink/p/8734103.html#DDOS)

- [CSRF](https://www.cnblogs.com/morethink/p/8734103.html#CSRF)



## 跨域

跨域：指的是浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏览器对JavaScript施加的安全限制。所谓同源是指，域名，协议，端口均相同。

#### 解决方式

一：使用JSONP访问

Jsonp是一种json访问的模式，其主要使用方式是用来对json的使用模式，是用来解决主流浏览器的跨域数据访问的问题。但JSONP同样有一个弊端就是JSONP只能支GET访问。

二：使用代理

使用代理的含义是取消浏览器访问模式，将访问转发给后台进行访问，这样就能成功的绕过浏览器，自然不会出现什么跨域问题。

三：修改Header参数





## JSONP

JSON的纯字符数据格式可以简洁的描述复杂数据；JSON还被js原生支持，所以在客户端几乎可以随心所欲的处理这种格式的数据。

凡是拥有”src”这个属性的标签都拥有跨域的能力

web客户端通过与调用脚本一模一样的方式，来调用跨域服务器上动态生成的js格式文件（一般以JSON为后缀），显而易见，服务器之所以要动态生成JSON文件，目的就在于把客户端需要的数据装入进去。

为了便于客户端使用数据，逐渐形成了一种非正式传输协议，人们把它称作JSONP，该协议的一个要点就是允许用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。





## HTTP报文的结构

报文首部  空行  报文主体

https://www.jianshu.com/p/65bd69fa204d

请求报文：请求行、请求头部、空行、请求数据

![这里写图片描述](http://www.2cto.com/uploadfile/Collfiles/20160921/20160921092902554.png)

其中请求行：请求方法字段  URL字段  HTTP协议版本字段（用空格分割）

​                    GET /data/info.html HTTP/1.1

其中HTTP协议版本有两种：HTTP1.0/HTTP1.1 可以这样区别：

HTTP1.0对于每个连接都只能传送一个请求和响应，请求就会关闭，HTTP1.0没有Host字段;而HTTP1.1在同一个连接中可以传送多个请求和响应，多个请求可以重叠和同时进行，HTTP1.1必须有Host字段。





## Http报文首部

![img](https://upload-images.jianshu.io/upload_images/11725889-41849e32943c5fbe.png?imageMogr2/auto-orient/strip|imageView2/2/w/1026/format/webp)



![img](https://upload-images.jianshu.io/upload_images/11725889-c306089867f51566.png?imageMogr2/auto-orient/strip|imageView2/2/w/1013/format/webp)

## HTTP通用首部字段

- Cache-Control: 对于缓存服务器下达缓存控制的相关指令，具体指令有`no-cache`, `no-store`, `max-age = ${秒}` , `public`, `private`等。
- Connection: 控制代理不再转发的字段，管理持久连接。
  如`Connection:Upgrade`，那么在经过代理后，Upgrade首部字段将不会被发送至服务器。如`Connection:Keep-Alive`。
- Date: 表示HTTP报文创建时间，如`Date:Fri, 19 Oct 2018 09:45:13 GMT`。
- Pragma: 兼容HTTP1.1以前的版本，控制缓存，如`Pragma:no-cache`。
- Transfer-Encoding: 报文传输时的编码方式，HTTP1.1仅对分块传输的编码形式有效，如`Transfer-Encoding:chunked`。

https://www.jianshu.com/p/65bd69fa204d

## 请求首部字段

- Accept系: 定义请求结果的要求，如Accept，Accept-Encoding，Accept-Language，Accept-Charset等。
- Host: 目标服务器的域和端口号，如`Host:www.demo.com`。
- Referer: 发起请求的页面URI，即`Referer:${window.location.href}`
- User-Agent: 客户端信息，如`User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36`

https://www.jianshu.com/p/65bd69fa204d

## 响应首部字段

- ETag: 某一个固定的URI资源发生变化时，ETag会更新，如`ETag:W/"92d8a6509d07d749ee661d8af47d2fbd"`
- Server: HTTP服务器的应用程序信息，如`Server:Apache/2.2.6 (Unix) PHP/5.2.5`
- Location: 引导客户端向某资源发起访问，一般配合状态码3xx使用，重定向请求，如`Location:http://www.demo2.com/index.html`。
- WWW-Authenticate: 告诉客户端认证方案，一般配合状态码`401 Unauthorized`使用，如`WWW-Authenticate:Basic realm="Usagidesign Auth"`

https://www.jianshu.com/p/65bd69fa204d

## 实体首部字段

- Allow: 资源允许的请求方式，如`Allow:GET, HEAD`。
- Expires: 资源过期时间，如`Expires:Fri, 20 Oct 2018 09:45:13 GMT`。
- Last-Modified: 资源最后一次修改的时间，如`Last-Modified:Fri, 15 Oct 2018 09:45:13 GMT`。
  还有一些表示资源具体信息的，如`Content-Encoding`, `Content-Type`, `Content-Language`, `Content-Range`等。

https://www.jianshu.com/p/65bd69fa204d

## Cookie相关首部字段

**Cookie相关，未被编入HTTP1.1 RFC2616标准中。****

Cookie: 属于请求首部，携带符合条件的Cookie（domain，path，expires）发送至服务器。
Set-Cookie: 属于响应首部，告诉客户端需要保存哪些Cookie值，包括要种Cookie的domain，path，expires。

除了文中所列举的首部字段之外，还有很多其他的首部字段，感兴趣的朋友可以通过其他文章或资料来学习。

https://www.jianshu.com/p/65bd69fa204d



## **HTTPS和HTTP的区别：**

**1、https协议需要到ca申请证书，一般免费证书较少，因而需要一定费用。**

**2、http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。**

**3、http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。**

**4、http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。**





## 常见的WEB攻击分类

#### 攻击类型

- [XSS](https://github.com/huyaocode/webKnowledge/blob/master/Web安全/XSS.md) 跨站脚本攻击
- [CSRF](https://github.com/huyaocode/webKnowledge/blob/master/Web安全/CSRF.md) 跨站请求伪造
- [SQL注入](https://github.com/huyaocode/webKnowledge/blob/master/Web安全/SQL注入.md)
- 点击劫持
- 中间人攻击

#### 安全问题

- 用户身份被盗用
- 用户密码泄露
- 用户资料被盗取
- 网站数据库泄露

#### 点击劫持

点击劫持是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 iframe 嵌套的方式嵌入自己的网页中，并将 iframe 设置为透明，在页面中透出一个按钮诱导用户点击。

对于这种攻击方式，推荐防御的方法有两种。

- X-FRAME-OPTIONS
- JS 防御

###### X-FRAME-OPTIONS

`X-FRAME-OPTIONS` 是一个 HTTP 响应头，在现代浏览器有一个很好的支持。这个 HTTP 响应头 就是为了防御用 iframe 嵌套的点击劫持攻击。

该响应头有三个值可选，分别是

- `DENY`，表示页面不允许通过`iframe`的方式展示
- `SAMEORIGIN`，表示页面可以在相同域名下通过`iframe`的方式展示
- `ALLOW-FROM`，表示页面可以在指定来源的`iframe`中展示

###### JS防御

对于某些低版本浏览器来说，并不能支持上面的这种方式，那我们只有通过 JS 的方式来防御点击劫持了。

```
<head>
  <style id="click-jack">
    html {
      display: none !important;
    }
  </style>
</head>
<body>
  <script>
    if (self == top) {
      var style = document.getElementById('click-jack')
      document.body.removeChild(style)
    } else {
      top.location = self.location
    }
  </script>
</body>
```

###### 中间人攻击

中间人攻击是攻击方同时与服务端和客户端建立起了连接，并让对方认为连接是安全的，但是实际上整个通信过程都被攻击者控制了。攻击者不仅能获得双方的通信信息，还能修改通信信息。

通常来说不建议使用公共的 Wi-Fi，因为很可能就会发生中间人攻击的情况。如果你在通信的过程中涉及到了某些敏感信息，就完全暴露给攻击方了。

当然防御中间人攻击其实并不难，只需要增加一个安全通道来传输信息。HTTPS 就可以用来防御中间人攻击，但是并不是说使用了 HTTPS 就可以高枕无忧了，因为如果你没有完全关闭 HTTP 访问的话，攻击方可以通过某些方式将 HTTPS 降级为 HTTP 从而实现中间人攻击。



#### SQL 注入

所谓SQL注入，就是通过把SQL命令插入到Web表单提交或输入域名或页面请求的查询字符串，后台执行SQL语句时直接把前端传入的字段拿来做SQL查询。

###### 防御

- 永远不要信任用户的输入。
- 永远不要使用动态拼装sql
- 不要把机密信息直接存放



#### XSS跨脚本攻击

XSS ( Cross Site Scripting ) 是指恶意攻击者利用网站没有对用户提交数据进行转义处理或者过滤不足的缺点，进而添加一些代码，嵌入到web页面中去。使别的用户访问都会执行相应的嵌入代码。

从而盗取用户资料、利用用户身份进行某种动作或者对访问者进行病毒侵害的一种攻击方式。

#### XSS攻击的危害包括：

1. 获取页面数据
2. 获取cookie
3. 劫持前端逻辑
4. 发送请求
5. 偷取网站任意数据
6. 偷取用户资料
7. 偷取用户密码和登陆态
8. 欺骗用户

[https://github.com/huyaocode/webKnowledge/blob/master/Web%E5%AE%89%E5%85%A8/XSS.md](https://github.com/huyaocode/webKnowledge/blob/master/Web安全/XSS.md)




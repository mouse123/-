# 网络协议

### HTTPS 是怎么工作的

* 简单的来说 HTTPS 的 S，就是 SSL/ TLS，SSL 是 TLS 的前身，基本上我们当成同一个 （S）看就行，换言之，HTTPS = HTTP + SSL / TLS，在 TCP 层到 HTTP 层之间加了一层 SSL。

  如图所示，在 HTTP 网站通讯中，由于没有一个三方认证的过程：

  ![avatar](https://raw.githubusercontent.com/mouse123/my-tips/master/image/http.jpg)

你完全无法得知，你收到的结果是否是被篡改后的结果，当然，更无法保证，即使没动过的数据，是不是会被窃听。 我们叫图中那位黑客「中间人」，也就会造成上文所说的中间人攻击。 因此后来，大家就想到了，只要手握一份密钥，是否就天下我有了？ 常见的加密有两种：对称加密和非对称加密——但是我们实际上发现，无论用对称加密还是非对称加密，密钥一泄露，还是没办法（对称加密比较快，但一份密钥非常容易泄露，在非对称加密中，公钥本身是公开的，只要截取私钥返回，需要公钥解密的部分，照样的截获数据）。 于是乎，我们又想到了一种升级的加密方式：对称与非对称结合。 ![avatar](https://raw.githubusercontent.com/mouse123/my-tips/master/image/encrypt%20http.jpg) 然后就变成了上图中的加密方式，我先用非对称加密的方式传输密钥，然后用对称加密传输数据，这样就可以避免了传输过程中对称加密密钥泄露和公钥公开导致的截获数据两个问题了——但是，怎么证明你是个好人呢？ 于是，终于找到了一个可信的三方机构：证书发布机构。

浏览器会在发起请求时帮你检验这个网站证书中的信息是否合法，是否是由授信机构发布的，如果不合法，那么就会报错，如果合法，那么就用对应颁发者的 CA 公钥解密，对服务器证书的签名解密。 之后使用 Hash 算法计算得到的证书和服务器发来的证书对应 Hash 是否一致，如果一致，代表没有被冒充。 之后读取证书中的密钥，用于后续加密通讯。 最终，我们的整个过程都不怕窃听篡改了——不过，可能有个让人困惑的问题，我的操作系统是怎么拥有这么多 CA 公钥的。 实际上，顶级的 CA 屈指可数，那些其他签发商，其实是被间接信任的，正好在前几天，Let's Encrypt 发布了一条消息，说明他们未来会被所有主要的程序直接信任，而过去，他们一直是被间接信任的，是由于浏览器和操作系统信任 IdenTrust，而 IdenTrust 信任他们，因此他们才被信任： Browsers and operating systems have not, by default, directly trusted Let’s Encrypt certificates, but they trust IdenTrust, and IdenTrust trusts us, so we are trusted indirectly. IdenTrust is a critical partner in our effort to secure the Web, as they have allowed us to provide widely trusted certificates from day one.

### 对称加密与非对称加密

* [对称加密与非对称加密](https://www.zhihu.com/question/33645891/answer/57721969)

### 安全相关

* [开发安全相关](https://github.com/FallibleInc/security-guide-for-developers/blob/master/security-checklist.md)

### Socket.io

socket.io 是一个基于websocket实现的前后端实时通讯框架，也对低版本浏览器做了封装。使用起来简单，方便。

初次使用起来可能会比较迷糊，其实主要常用就几个方法，简单介绍一下。

**客户端**

io.connect\(url\) //客户端连接上服务器端

**socket**.on\('eventName', msg =&gt; {}\) //客户端监听服务器端事件

**socket**.emit\('eventName', msg\) //客户端向服务器端发送数据

socket.disconnect\(\) //客户端断开链接

**服务端**

socket.on\('eventName', msg =&gt; {}\) //服务器端监听客户端emit的事件，事件名称可以和客户端是重复的，但是并没有任何关联。socket.io内置了一些事件比如connection，disconnect，**exit**事件，业务中错误处理需要用到。

**socket**.emit\('eventName', msg\) //服务端各自的socket向各自的客户端发送数据

**socket**.broadcast\('eventName', msg\) //服务端向其他客户端发送消息，不包括自己的客户端

socket.**join**\(channel\) //创建一个频道（非常有用，尤其做分频道的时候，比如斗地主这种实时棋牌游戏）

io.sockets.in\(channel\) //加入一个频道

socket.broadcast.to\(channel\).emit\('eventName', msg\) //向一个频道发送消息，不包括自己

io.sockets.adapter.rooms //获取所有的频道

### 其他

* https \(CERT\_HAS\_EXPIRED\)证书过期的错误请求
  * 解决方法:请求options添加改属性 rejectUnauthorized: false
* gzip http传输
* HTTP请求 host 需要dns域名解析，若解析失败，则导致无法发起http请求
* [HTTP2](https://zhuanlan.zhihu.com/p/29609078)


# Cookie和Session
---

> Cookie

  Cookie是由服务器发送给客户端的小量信息，以{key: value}形式的存在


> Cookie 机制原理

  客户端请求服务器时，如果服务器需要记录该用户状态，就使用response向客户端浏览器颁发一个Cookie。而客户端浏览器会把Cookie保存起来。当浏览器再请求 服务器时，浏览器把请求的网址连同该Cookie一同提交给服务器。服务器通过检查该Cookie来获取用户状态。

  ---

> Session

  Cookie机制弥补了HTTP协议无状态的不足。在Session出现之前，基本上所有的网站都采用Cookie来跟踪会话。
  与Cookie不同的是，session是以服务端保存状态的。

> session机制原理

  当客户端请求创建一个session的时候，服务器会先检查这个客户端的请求里是否已包含了一个session标识 - sessionId，

  + 如果已包含这个sessionId，则说明以前已经为此客户端创建过session，服务器就按照sessionId把这个session检索出来使用（如果检索不到，可能会新建一个）

  + 如果客户端请求不包含sessionId，则为此客户端创建一个session并且生成一个与此session相关联的sessionId

  sessionId的值一般是一个既不会重复，又不容易被仿造的字符串，这个sessionId将被在本次响应中返回给客户端保存。保存sessionId的方式大多情况下用的是cookie。

  ---
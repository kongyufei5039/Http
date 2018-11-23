#### 1.客户端请求服务端响应
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.004.png)  

> 客户端发送给某个 HTTP 服务器端的请求报文中的内容  
`GET /index.htm HTTP/1.1`  
`Host: hackr.jp`  

![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.005.png)

> 服务端响应客户端的内容  
`HTTP/1.1 200 OK`  
`Date: Tue, 10 Jul 2012 06:50:15 GMT`
`Content-Length: 362`  
`Content-Type: text/html`  
`<html>`  
`......`

![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.006.png)

#### 2.HTTP 是不保存状态的协议
HTTP 是一种不保存状态，即无状态（stateless）协议。协议本身并不保留之前一切的请求或响应报文的信息。这是为了更快地处理大量事务，确保协议的可伸缩性，而特意把 HTTP 协议设计成如此简单的。

#### 3.使用 Cookie 的状态管理
HTTP/1.1 虽然是无状态协议，但为了实现期望的保持状态功能，于是引入了 Cookie 技术。  

Cookie 会根据从服务器端发送的响应报文内的一个叫做 Set-Cookie 的首部字段信息，通知客户端保存 Cookie。当下次客户端再往该服务器发送请求时，客户端会自动在请求报文中加入 Cookie 值后发送出去。  

服务器端发现客户端发送过来的 Cookie 后，会去检查究竟是从哪一个客户端发来的连接请求，然后对比服务器上的记录，最后得到之前的状态信息。

* 没有 Cookie 信息状态下的请求  
![](http://images.gitbook.cn/d8263ca0-3ba4-11e8-9f33-a7686c32808c)  
* 第 2 次以后（存有 Cookie 信息状态）的请求  
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.024.png)  

> 1.请求报文（没有 Cookie 信息的状态）  
`GET /reader/ HTTP/1.1`  
`Host: hackr.jp`  
*首部字段内没有Cookie的相关信息

> 2.响应报文（服务器端生成 Cookie 信息）  
`HTTP/1.1 200 OK`  
`Date: Thu, 12 Jul 2012 07:12:20 GMT`  
`Server: Apache`  
`＜Set-Cookie: sid=1342077140226724; path=/; expires=Wed,10-Oct-12 07:12:20 GMT＞`  
`Content-Type: text/plain; charset=UTF-8`  

> 3.请求报文（自动发送保存着的 Cookie 信息）  
`GET /image/ HTTP/1.1`  
`Host: hackr.jp`  
`Cookie: sid=1342077140226724`  

#### 4.使用方法下达命令
方法中有 GET、POST 和 HEAD 等。  
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.017.png)

#### 5.持久连接节省通信量
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.018.png)
每次通信结束都断开TCP连接，下次通信又重新建立TCP连接，增加了通信量的开销。  

为解决上述 TCP 连接的问题，HTTP/1.1 和一部分的 HTTP/1.0 想出了持久连接（HTTP Persistent Connections，也称为 HTTP keep-alive 或 HTTP connection reuse）的方法。持久连接的特点是，只要任意一端没有明确提出断开连接，则保持 TCP 连接状态。
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.020.png)  
 
#### 6.管线化
持久连接使得多数请求以管线化（pipelining）方式发送成为可能。从前发送请求后需等待并收到响应，才能发送下一个请求。管线化技术出现后，不用等待响应亦可直接发送下一个请求。
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/06.d02z.021.png)

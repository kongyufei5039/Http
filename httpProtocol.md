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
#### 1.Web构建技术
> * URL（Uniform Resource Locator，统一资源定位符）
> * HTML（HyperText Markup Language，超文本标记语言）
> * HTTP（HyperText Transfer Protocol，超文本传输协议）

#### 2.网络基础 TCP/IP

##### 2.1 TCP/IP 协议族
定义\([维基百科](https://zh.wikipedia.org/wiki/TCP/IP%E5%8D%8F%E8%AE%AE%E6%97%8F#TCP/IP%E5%8D%94%E8%AD%B0%E6%A3%A7%E7%B5%84%E6%88%90)\)

##### 2.2 TCP/IP 的分层管理
* 应用层  
应用层决定了向用户提供应用服务时通信的活动。  
例如：HTTP（超文本传输协议）、SMTP（简单邮件传输协议）、FTP（文件传输协议）、SSH（加密的网络传输协议）
* 传输层  
传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。  
例如：TCP（传输控制协议）、UDP（用户数据报协议）  
  > TCP和UDP的区别  

  > TCP是一种面向连接的、可靠的、基于字节流的传输层通信协议。应用场景举例：浏览器用的HTTP，传输文件用的FTP，发送邮件用的POP、SMTP，加密传输用的SSH  
  UDP是一个简单的面向数据报的传输层协议，只提供数据的不可靠传递，它一旦把应用程序发给网络层的数据发送出去，就不保留数据备份。应用场景举例：即时通讯，在线视频，网络语音电话

* 网络层（又名网络互连层）  
网络层用来处理在网络上流动的数据包。数据包是网络传输的最小数据单位。

* 链路层（又名数据链路层，网络接口层）  
用来处理连接网络的硬件部分。

#### 2.3 TCP/IP 通信传输流
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.006.png)



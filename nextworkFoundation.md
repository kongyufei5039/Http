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

#### 3 TCP/IP 通信传输流
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.006.png)  
利用 TCP/IP 协议族进行网络通信时，会通过分层顺序与对方进行通信。发送端从应用层往下走，接收端则从链路层往上走。  
我们用 HTTP 举例来说明，首先作为发送端的客户端在应用层（HTTP 协议）发出一个想看某个 Web 页面的 HTTP 请求。  
接着，为了传输方便，在传输层（TCP 协议）把从应用层处收到的数据（HTTP 请求报文）进行分割，并在各个报文上打上标记序号及端口号后转发给网络层。  
在网络层（IP 协议），增加作为通信目的地的 MAC 地址后转发给链路层。这样一来，发往网络的通信请求就准备齐全了。  
接收端的服务器在链路层接收到数据，按序往上层发送，一直到应用层。当传输到应用层，才能算真正接收到由客户端发送过来的 HTTP 请求。  
![](http://images.gitbook.cn/0c5f9240-3ba6-11e8-9769-ad5a3e0d00fa)  
发送端在层与层之间传输数据时，每经过一层时必定会被打上一个该层所属的首部信息。反之，接收端在层与层传输数据时，每经过一层时会把对应的首部消去。  
这种把数据信息包装起来的做法称为封装（encapsulate）。  

#### 4 与 HTTP 关系密切的协议：IP、TCP 和 DNS

##### 4.1负责传输的 IP 协议
IP（Internet Protocol，网际协议）\([维基百科](https://zh.wikipedia.org/wiki/%E7%BD%91%E9%99%85%E5%8D%8F%E8%AE%AE)\)  
IP 协议的作用是把各种数据包传送给对方。而要保证确实传送到对方那里，则需要满足各类条件。其中两个重要的条件是 IP 地址和 MAC 地址（Media Access Control Address）。  
IP 地址指明了节点被分配到的地址，MAC 地址是指网卡所属的固定地址。IP 地址可以和 MAC 地址进行配对。IP 地址可变换，但 MAC 地址基本上不会更改。  
* 使用 ARP 协议凭借 MAC 地址进行通信  
IP 间的通信依赖 MAC 地址。在网络上，通信的双方在同一局域网（LAN）内的情况是很少的，通常是经过多台计算机和网络设备中转才能连接到对方。而在进行中转时，会利用下一站中转设备的 MAC 地址来搜索下一个中转目标。这时，会采用 ARP 协议（Address Resolution Protocol）。ARP 是一种用以解析地址的协议，根据通信方的 IP 地址就可以反查出对应的 MAC 地址。

##### 4.2确保可靠性的 TCP 协议
TCP（Transmission Control Protocol，传输控制协议）\([维基百科](https://zh.wikipedia.org/wiki/%E4%BC%A0%E8%BE%93%E6%8E%A7%E5%88%B6%E5%8D%8F%E8%AE%AE)\)  
按层次分，TCP 位于传输层，提供可靠的字节流服务。  
所谓的字节流服务（Byte Stream Service）是指，为了方便传输，将大块数据分割成以报文段（segment）为单位的数据包进行管理。而可靠的传输服务是指，能够把数据准确可靠地传给对方。一言以蔽之，TCP 协议为了更容易传送大数据才把数据分割，而且 TCP 协议能够确认数据最终是否送达到对方。
* 确保数据能到达目标  
为了准确无误地将数据送达目标处，TCP 协议采用了三次握手（three-way handshaking）策略。用 TCP 协议把数据包送出去后，TCP 不会对传送后的情况置之不理，它一定会向对方确认是否成功送达。握手过程中使用了 TCP 的标志（flag） —— SYN（synchronize） 和 ACK（acknowledgement）。  
发送端首先发送一个带 SYN 标志的数据包给对方。接收端收到后，回传一个带有 SYN/ACK 标志的数据包以示传达确认信息。最后，发送端再回传一个带 ACK 标志的数据包，代表“握手”结束。  
若在握手过程中某个阶段莫名中断，TCP 协议会再次以相同的顺序发送相同的数据包。
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.009.png)

##### 4.3负责域名解析的 DNS 服务
DNS（Domain Name System，域名系统）\([维基百科](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F)\)  
DNS 协议提供通过域名查找 IP 地址，或逆向从 IP 地址反查域名的服务。
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.010.png)  

#### 5各种协议与 HTTP 协议的关系
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.011.png)



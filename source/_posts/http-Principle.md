---
title: http原理
typora-root-url: ../ArrayNot/
date: 2019-07-29 21:00:41
tags: [http,原理]
---
名词说明：

* HTTP（HyperText Transfer Protocol）超文本传输协议
* SGML（Standard Generalized Markup Language）标准通用标记语言
* URL（Uniform Resource Locator）统一资源定位符
* URI（Uniform Resource Identifer）统一资源标识符
* TCP（Transmission Control Protocol）传输控制协议
* IP（Internet Protocol）网际协议
* UDP（User Data Protocol）用户数据报协议
* MAC地址（Media Access Control）媒体访问控制地址／物理地址／硬件地址
* ARP协议（Address Resolution Protocol）地址解析协议

![image text](344f679609.jpg)

<!--more-->



---
### 基础
<b>TCP/IP</b>

TCP/IP是互联网相关的各类协议族的总称，而HTTP是TCP/IP协议族中的一个子集。

TCP/IP协议族可以分为以下四层：
* 应用层(决定了向用户提供应用服务时通信的活动。TCP/IP协议族内预存了各类通用的应用服务，如HTTP、FTP、DNS等)
* 传输层(提供处于网络连接中的两台计算机之间的数据传输。包含两个协议：TCP、UDP)
* 网络层(或网络互连层。用来处理网络上流动的数据包，在众多的选项中选择一条传输线路，将数据包传送到对方计算机。包含的协议如：IP协议
* 数据链路层(或链路层、网络接口层。用来处理连接网络的硬件部分)
  
 <b>TCP协议</b>
TCP协议位于传输层，提供可靠的字节流服务(即将大数据块分割成以报文段为单位的数据包进行管理)。

为了确保数据准确无误的到达目标处，TCP协议通常采用三次握手策略。

![image text](http-Principle/6e7.png)

若在握手过程中某个阶段莫名中断，TCP协议会再次以相同的顺序发送相同的数据包。

<b>IP协议</b>

IP协议位于网络层，负责将各种数据包传送给对方，为了保证确实传送成功，需要满足各类条件，其中两个重要的条件是IP地址和MAC地址。
* IP地址，指明了节点被分配到的地址
* MAC地址，指网卡所属的固定地址
* IP地址可以和MAC地址进行配对，IP地址可以变换，但是MAC地址基本上不会更改
* 使用ARP地址解析协议可以根据通信方的IP地址反查出对应的MAC地址

<b>DNS协议</b>
DNS协议位于应用层，提供域名到IP地址之间的解析服务。

<b>URI与URL</b>
URI是由某个协议方案表示的资源的定位标识符，协议方案是指访问资源所使用的协议类型名称，如http、ftp、file等。

URI用字符串标识某一互联网资源，而URL表示资源的地点，URL是URI的子集。

### HTTP协议

HTTP协议用于客户端和服务器端之间的通信。请求必定由客户端发出，而服务器端回复响应。
* 客户端：请求文本或图像等资源
* 服务器端：提供资源响应

HTTP协议不保存状态，为无状态协议。这是为了更快的处理大量事务，确保协议的可伸缩性而特意设计的。但是随着Web的不断发展，这一特性也引发了一些问题，如：如何保持登录状态、如何记录用户信息等，为了解决这一问题，引入了Cookie技术。

HTTP协议通过URI定义资源

<b>HTTP报文</b>

用于HTTP协议交互的信息被称为报文。报文由报文首部、空行(CR+LF)、报文主体组成。

* 请求报文，客户端发送请求的报文。请求报文首部由请求行、请求首部字段、通用首部字段、实体首部字段以及其他组成
* 响应报文，服务器端响应的报文。响应报文首部由状态行、响应首部字段、通用首部字段、实体首部字段以及其他组成

<b>HTTP首部字段</b>

HTTP首部字段是构成HTTP报文的要素之一，在客户端与服务器之间以HTTP协议进行通讯的过程中，无论是请求还是响应都会使用首部字段，它能起到传递额外终于信息的作用。使用首部字段是为了给浏览器和服务器提供报文主体大小、所使用的语言、认证信息等内容。

<b>HTTP方法</b>

方法名称	|方法描述
:----:|:----
GET	|获取资源
POST|	传输实体主体
PUT	|传输文件，自身不带验证机制 ，在无验证机制或不遵守REST标准时不建议使用
DELETE|	删除文件，自身不带验证机制
HEAD	|获取报文首部，和GET方法一样，不返回报文主体部分
OPTIONS	|询问支持的方法，返回服务器所支持的方法
TRACE	|追踪路径，可以通过该方法查询发送出去的请求是如何被加工修改或篡改的。容易引发XST攻击，不常用。
CONNECT	|要求用隧道协议连接代理


<b>HTTP状态码</b>

状态码用来描述请求的结果

* 1XX Informational 信息性状态码，接收的请求正在处理
* 2XX Success 成功状态码，请求正常处理完毕
* 3XX Redirection 重定向状态码，需要进行附加操作以完成请求
* 4XX Client Error 客户端错误状态码，服务器无法处理请求
* 5XX Server Error 服务器错误状态码，服务器处理请求出错

常用的状态码：

状态码	|状态内容|	状态描述
:----:|:----:|:----
200	|OK	|表示客户端的请求在服务器端被正常处理
204	|No Condent	|表示请求被成功处理，但是不返回任何实体的主体，在浏览器中表现为页面不发生更新
206	|Partial Condent	|表示客户端进行了范围请求，且服务器成功执行了这部分的GET请求
301	|Moved Permanently	|永久性重定向，表示请求的资源已经被分配了新的URI，以后应使用新的URI访问
302	|Found	|临时性重定向，表示请求的资源已经被分配了新的URI，希望用户本次使用新的URI访问
303	|See Other	|与302功能相同，但是303状态码明确表示客户端应采用GET方法获取资源
304	|Not Modified	|表示客户端发送附带条件的请求时，服务器端允许访问资源，但当条件不满足时，返回304状态码
307	|Temporary Redirect	|临时重定向，与302状态码含义相同，307状态码会遵照浏览器标准，不会从POST变成GET，但是对于处理相应时的行为，每种浏览器有可能出现不同的情况
400	|Bad Request	|表示请求报文中存在语法错误
401	|Unauthorized	|表示需要有HTTP认证的认证信息或者用户认证失败
403	|Forbidden	|表示对请求资源的访问被服务器拒绝了
404	|Not Found	|表示服务器上无法找到请求的资源
500	|Internal Server Error	|表示服务器在执行请求时发生了错误或者web应用存在的bug或者某些临时故障
503	|Service Unavailable	|表示服务器暂时处于超负载或者正在停机维护，无法处理请求
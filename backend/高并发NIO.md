
#### 深入理解高并发NIO底层原理及并发模型

分布式：通信+数据结构+算法
高并发、高性能的关键之一

OSI七层网络模型
程序员：应用层（TFTP、HTTP、SNMP、FTP、SMTP、Telnet） + 内核层

##### 怎么通过IO库调用内核？
不同语言（java、c++、c）调用内核，socket网络编程
socket是对内核调用接口的封装

一次网络IO流程：数据准备 -》 数据拷贝
![](./reference/IO_网络io.JPG)

##### 深入分析3大linux IO内核模型
什么是io模型？
取决于应用如何调用内核io函数。
阻塞、非阻塞；同步，异步

5大IO模型
阻塞IO
非阻塞IO
IO多路复用  //NIO(New IO)
信号驱动
异步IO  //异步

文件描述符 fd，所有的OS资源（IO流、socket连接）抽象成文件

##### 理解同步、异步
强调结果返回形式
支付场景：调银行支付接口，传回调接口给银行，支付成功后通过回调接口返回

##### 理解阻塞、非阻塞
强调对`调用端`的影响

- 阻塞IO
![](./reference/IO_blocking.JPG)

- 非阻塞IO  
CPU异常
![](./reference/IO_noblocking.JPG)
开启监听accept -》 调用recvFrom

tomcat如何服务多个客户端连接？

- IO多路复用

应用层面需要实现selector()
多路复用器selector()， 多路即多个客户端通讯通道，复用器即调用Epoll()
大名鼎鼎epoll

BIO -> 基于线程驱动，1:1，N:N
一个客户端是一个线程

异步编程
![](./reference/IO_bio_demo.JPG)
优化：线程池，避免大量线程CPU资源耗尽

高并发场景下，瓶颈点：请求数量超过线程池

java 1.4出IO库
NIO -> 基于事件驱动  1个线程服务 N多个客户端请求
事件：接受、读、写、连接、断开

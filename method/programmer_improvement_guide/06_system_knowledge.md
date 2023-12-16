# 《程序员练级攻略》分析笔记

## 第6章 系统知识

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

介绍系统知识的学习方法及资料。

### Q3：这一章的大纲是什么

- 系统知识
- C10K 问题
- 实践项目

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 系统知识

- [《Computer Systems A Programmer’s Perspective》（中文版为《《深入理解计算机系统》》）][1]: 程序员必读。

- Richard Stevens 的 4 卷书
  - [《Unix 高级环境编程》][2]
  - [《Unix 网络编程·卷1：套接口 API》][3]
  - [《Unix 网络编程·卷2：进程间通信》][4]
  - [《TCP/IP 详解·卷1：协议》][5]

- 如果你觉得上面这几本经典书比较难啃，你可以试试下面这些通俗易懂的
  （当然，如果读得懂上面那三本的，下面的这些也就不需要读了）
  - [《Linux C 编程一站式学习》][6]
  - [《TCP/IP 网络编程》][7]
  - [《图解 TCP/IP][8]: 这本书其实并不是只讲了 TCP/IP，应该是叫《计算机网络》才对，主要是给想快速入门的人看的。
  - [《The TCP/IP Guide][9]: 这本书在豆瓣上的评分 9.2，这里给的链接是这本书的 HTML 英文免费版的，里面的图画得很精彩。

- [《Wireshark 数据包分析实战》][10]
  - 学习网络协议不单只是看书，你最好用个抓包工具看看这些网络包是什么样的。

- 看完《Unix 高级环境编程》后，你可以趁热打铁看看
  - [《Linux/Unix 系统编程手册》][11]
  - [《Linux System Programming》][12]: 主要突出的是 Linux 的一些关键技术和相关的系统调用。

- TCP 文章推荐
  - [Let’s code a TCP/IP stack, 1: Ethernet & ARP][13]
  - [Let’s code a TCP/IP stack, 2: IPv4 & ICMPv4][14]
  - [Let’s code a TCP/IP stack, 3: TCP Basics & Handshake][15]
  - [Let’s code a TCP/IP stack, 4: TCP Data Flow & Socket API][16]
  - [Let’s code a TCP/IP stack, 5: TCP Retransmission][17]

- 系统知识学习要点
  - 用这些系统知识操作一下文件系统，实现一个可以拷贝目录树的小程序。
  - 用 `fork / wait / waitpid` 写一个多进程的程序，用 `pthread` 写一个多线程带同步或互斥的程序。比如，多进程购票的程序。
  - 用 `signal / kill / raise / alarm / pause / sigprocmask` 实现一个多进程间的信号量通信的程序。
  - 学会使用 gcc 和 gdb 来编程和调试程序（参看我的[《用 gdb 调试程序》][18]）。
  - 学会使用 makefile 来编译程序（参看我的[《跟我一起写 makefile》][19]）。
  - Socket 的进程间通信。用 C 语言写一个 1 对 1 的聊天小程序，或是一个简单的 HTTP 服务器。

#### C10K 问题

- [C10K Problem][20]
  - [C10K 问题（中文翻译版）][21]

- C10K 问题的本质
  - C10K 问题本质上是操作系统处理大并发请求的问题。
  - 对于 Web 时代的操作系统而言，对于客户端过来的大量的并发请求，需要创建相应的服务进程或线程。
  - 这些进程或线程多了，导致数据拷贝频繁（缓存 I/O、内核将数据拷贝到用户进程空间、阻塞）， 进程 / 线程上下文切换消耗大，从而导致资源被耗尽而崩溃。

- C10M 问题
  - [《The Secret To 10 Million Concurrent Connections -The Kernel Is The Problem, Not The Solution》][22]

#### 实践项目

- 实践项目1：实现一个 telnet 版本的聊天服务器，主要有以下需求。
  - 每个客户端可以用使用 `telnet ip:port` 的方式连接到服务器上。
  - 新连接需要用用户名和密码登录，如果没有，则需要注册一个。
  - 然后可以选择一个聊天室加入聊天。
  - 管理员有权创建或删除聊天室，普通人员只有加入、退出、查询聊天室的权力。
  - 聊天室需要有人数限制，每个人发出来的话，其它所有的人都要能看得到。

- 实践项目2：实现一个简单的 HTTP 服务器，主要有以下需求。
  - 解释浏览器传来的 HTTP 协议，只需要处理 URL path。
  - 然后把所代理的目录列出来。
  - 在浏览器上可以浏览目录里的文件和下级目录。
  - 如果点击文件，则把文件打开传给浏览器（浏览器能够自动显示图片、PDF，或 HTML、CSS、JavaScript 以及文本文件）。
  - 如果点击子目录，则进入到子目录中，并把子目录中的文件列出来。

- 实践项目3：实现一个生产者 / 消费者消息队列服务，主要有以下需求。
  - 消息队列采用一个 Ring-buffer 的数据结构。
  - 可以有多个 topic 供生产者写入消息及消费者取出消息。
  - 需要支持多个生产者并发写。
  - 需要支持多个消费者消费消息（只要有一个消费者成功处理消息就可以删除消息）。
  - 消息队列要做到不丢数据（要把消息持久化下来）。能做到性能很高。

### Q7：作者是怎么论述的

### Q8：作者解决了什么问题

### Q9：我有哪些疑问

### Q10：这一章说得有道理吗？为什么

### Q11: 这一章讨论的知识的本质是什么

### Q12: 这一章讨论的知识的第一原则是什么

### Q13：这一章讨论的知识的结构是怎样的

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

### Q15：有哪些相似的知识？它们之间的联系是什么

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

### Q17: 这一章对我有哪些用处/帮助/启示

### Q18: 我如何应用这一章的知识去解决问题

  [1]: https://book.douban.com/subject/5333562/
  [2]: https://book.douban.com/subject/1788421/
  [3]: https://book.douban.com/subject/1500149/
  [4]: https://book.douban.com/subject/4118577/
  [5]: https://book.douban.com/subject/1088054/
  [6]: https://book.douban.com/subject/4141733/
  [7]: https://book.douban.com/subject/25911735/
  [8]: https://book.douban.com/subject/24737674/
  [9]: http://www.tcpipguide.com/free/index.htm
  [10]: https://book.douban.com/subject/21691692/
  [11]: https://book.douban.com/subject/25809330/
  [12]: http://igm.univ-mlv.fr/~yahya/progsys/linux.pdf
  [13]: https://book.douban.com/subject/25828773/
  [14]: http://www.saminiir.com/lets-code-tcp-ip-stack-1-ethernet-arp/
  [15]: http://www.saminiir.com/lets-code-tcp-ip-stack-2-ipv4-icmpv4/
  [16]: http://www.saminiir.com/lets-code-tcp-ip-stack-3-tcp-handshake/
  [17]: http://www.saminiir.com/lets-code-tcp-ip-stack-4-tcp-data-flow-socket-api/
  [18]: https://wiki.ubuntu.org.cn/%E7%94%A8GDB%E8%B0%83%E8%AF%95%E7%A8%8B%E5%BA%8F
  [19]: https://seisman.github.io/how-to-write-makefile/Makefile.pdf
  [20]: http://www.kegel.com/c10k.html
  [21]: https://www.oschina.net/translate/c10k
  [22]: http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html

# 《程序员练级攻略》分析笔记

## 第8章 Linux 系统、内存和网络

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- Linux 系统相关
- 内存相关
- 计算机网络
  - 网络学习
  - 网络调优
  - 网络协议

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### Linux 系统相关

- [Red Hat Enterprise Linux 文档][1]: Red Hat 网站上的这个文档中有很多很有价值的内容，值得一看。
- [Linux Insides][2]: GitHub 上的一个开源电子书，其中讲述了 Linux 内核是怎样启动、初始化以及进行管理的。
- [LWN’s kernel page][3]: 上面有很多非常不错的文章来解释 Linux 内核的一些东西。
- [Learn Linux Kernel from Android Perspective][4]: 从 Android 的角度来学习 Linux 内核，这个站点上的 Blog 相对于前面的比较简单易读一些。
- [Linux Kernel Do][5]:  Linux 的内核文档也可以浏览一下。
- [Kernel Planet][6]: Linux 内核开发者的 Blog，有很多很不错的文章和想法。
- [Linux Performance and Tuning Guidelines][7]: 这是 IBM 出的红皮书，虽然有点老了，但还是非常值得一读的。
- [TLK: The Linux Kernel][8]: 这是一本相对比较老的书了，Linux 内核版本为 2.0.33，但了解一下前人的思路，也是很有帮助的。
- [Linux Performance][9]: 这个网站上提供了和 Linux 系统性能相关的各种工具和文章收集，非常不错。
- [Optimizing web servers for high throughput and low latency][10]: 这是一篇非常底层的系统调优的文章，来自 DropBox，从中你可以学到很多底层的性能调优的经验和知识。

#### 内存相关

- [What every programmer should know about memory][11]
  - [Part 1: Introduction][12]
  - [Part 2: CPU caches][13]
  - [Part 3 (Virtual memory)][14]
  - [Part 4 (NUMA systems)][15]
  - [Part 5 (What programmers can do - cache optimization)][16]
  - [Part 6 (What programmers can do - multi-threaded optimizations)][17]
  - [Part 7 (Memory performance tools)][18]
  - [Part 8 (Future technologies)][19]
  - [Part 9 (Appendices and bibliography)][20]

- 几篇和内存相关的论文（对性能优化很有帮助）
  - [Memory Barriers: a Hardware View for Software Hackers][21]
    - 内存的读写屏障是线程并发访问共享的内存数据时，从程序本身、编译器到 CPU 都必须遵循的一个规范。
    - 有了这个规范，才能保证访问共享的内存数据时，一个线程对该数据的更新能被另一个线程以正确的顺序感知到。
    - 在 SMP（对称多处理）这种类型的多处理器系统（包括多核系统）上，这种读写屏障还包含了复杂的缓存一致性策略。这篇文章做了详细解释。
  - [A Tutorial Introduction to the ARM and POWER Relaxed Memory Models][22]
    - 对 ARM 和 POWER 的宽松内存模型的一个教程式的简介。
    - 本篇文章的焦点是 ARM 和 POWER 体系结构下多处理器系统内存并发访问一致性的设计思路和使用方法。
    - 与支持较强的 TSO 模型的 x86 体系结构不同，ARM 和 POWER 这两种体系结构出于对功耗和性能的考虑，使用了一种更为宽松的内存模型。
    - 本文详细讨论了 ARM 和 POWER 的模型。
  - [x86-TSO: A Rigorous and Usable Programmer’s Model for x86 Multiprocessors][23]
    - 介绍 x86 的多处理器内存并发访问的一致性模型 TSO。

- 内存管理方面的 lib 库：通常来说，我们有三种内存分配管理模块。就目前而言，BSD 的 jemalloc 有很大的影响力。
  - [ptmalloc][24] 是 glibc 的内存分配管理。
  - [tcmalloc][25] 是 Google 的内存分配管理模块，全称是 Thread-Caching malloc，基本上来说比 glibc 的 ptmalloc 快两倍以上。
  - [jemalloc][26] 是 BSD 提供的内存分配管理。其论文为 [A Scalable Concurrent malloc(3) Implementation for FreeBSD][27]，这是一个可以并行处理的内存分配管理器。

- 三种内存分配器的一些比较和工程实践
  - [ptmalloc，tcmalloc 和 jemalloc 内存分配策略研究][28]
  - [内存优化总结：ptmalloc、tcmalloc 和 jemalloc][29]
  - [Scalable memory allocation using jemalloc][30]
  - [Decreasing RAM Usage by 40% Using jemalloc with Python & Celery][31]

#### 计算机网络

##### 网络学习

- 书籍推荐：[《计算机网络（第五版）》][32]

- 网上的两个入门教程和讲义
  - 渥汰华大学的一个课程讲义：[Computer Network Design][33]
  - GeeksforGeeks 的一个简单的教程： [Computer Network Tutorials][34]

##### 网络调优

- 《Linux 的高级路由和流量控制 HowTo》（[Linux Advanced Routing & Traffic Control HOWTO][35]）
  - 这是一个非常容易上手的关于 iproute2、流量整形和一点 netfilter 的指南。

- 网络调优文档：[Red Hat Enterprise Linux Network Performance Tuning Guide][36]

- 网络工具列表：[Awesome Pcap Tools][37]
  - 其中罗列了各种网络工具，能够让你更从容地调试网络相关的程序。

- TCP 调优论文：[Making Linux TCP Fast][38]

- PackageCloud 上的两篇关于 Linux 网络栈相关的底层文章
  - [Monitoring and Tuning the Linux Networking Stack: Receiving Data][39]
  - [Monitoring and Tuning the Linux Networking Stack: Sending Data][40]

##### 网络协议

- 第 2 层链路层，你可能需要了解一下：
  - ARP: [RFC 826 - An Ethernet Address Resolution Protocol][41]
  - Tunnel 相关协议：
    - [RFC 1853 - IP in IP Tunneling][42]
    - [RFC 2784 - Generic Routing Encapsulation (GRE)][43]
    - [RFC 2661 - Layer Two Tunneling Protocol “L2TP”][44]
    - [RFC 2637 - Point-to-Point Tunneling Protocol (PPTP)][45]

- 第 4 层传输层，你最需要了解的是 TCP/IP：
  - 酷壳上的两篇文章
    - [《TCP 的那些事儿（上）》][46]
    - [《TCP 的那些事儿（下）》][47]
  - RFC
    - [RFC 793 - Transmission Control Protocol][48]: 最初的 TCP 标准定义，但不包括 TCP 相关细节。
    - [RFC 813 - Window and Acknowledgement Strategy in TCP][49]: TCP 窗口与确认策略，并讨论了在使用该机制时可能遇到的问题及解决方法。
    - [RFC 879 - The TCP Maximum Segment Size and Related Topics][50]: 讨论 MSS 参数对控制 TCP 分组大小的重要性，以及该参数与 IP 分段大小的关系等。
    - [RFC 896 - Congestion Control in IP/TCP Internetworks][51]: 讨论拥塞问题和 TCP 如何控制拥塞。
    - [RFC 2581 - TCP Congestion Control][52]: 描述用于拥塞控制的四种机制：慢启动、拥塞防御、快重传和快恢复。
      后面这个 RFC 被 [RFC 5681][53] 所更新。
      还有 [RFC 6582 - The NewReno Modification to TCP’s Fast Recovery Algorithm][54] 中一个改进的快速恢复算法。
    - [RFC 2018 - TCP Selective Acknowledgment Options][55]: TCP 的选择确认。
    - [RFC 2883 - An Extension to the Selective Acknowledgement (SACK) Option for TCP][56]: 对于 RFC 2018 的改进。
    - [RFC 2988 - Computing TCP’s Retransmission Timer][57]: 讨论与 TCP 重传计时器设置相关的话题，重传计时器控制报文在重传前应等待多长时间。也就是经典的 TCP Karn/Partridge 重传算法。
    - [RFC 6298 - Computing TCP’s Retransmission Timer][58]: TCP Jacobson/Karels Algorithm 重传算法。
  - 我个人觉得 TCP 最牛的不是不丢包，而是拥塞控制。对此，如果你感兴趣，可以读一下经典论文[《Congestion Avoidance and Control》][59]。
  - 关于 Linux 下的 TCP 参数，你需要仔仔细细地读一下 [TCP 的 man page][60]。

- 第 7 层应用层，HTTP 协议是重点。
  - 首先推荐的是[《HTTP 权威指南 》][61]
    - 这本书有点厚，可以当参考书来看。这本书中没有提到 HTTP/2 的事，但是可以让你了解到 HTTP 协议的绝大多数特性。
  - RFC
    - [RFC 7230 - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing][62]
    - [RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content][63]
    - [RFC 7232 - Hypertext Transfer Protocol (HTTP/1.1): Conditional Requests][64]
    - [RFC 7233 - Hypertext Transfer Protocol (HTTP/1.1): Range Requests][65]
    - [RFC 7234 - Hypertext Transfer Protocol (HTTP/1.1): Caching][66]
    - [RFC 7235 - Hypertext Transfer Protocol (HTTP/1.1): Authentication][67]
  - HTTP2
    - [Wikipedia: HTTP2][68]
    - [Gitbook - HTTP/2 详解][69] （原链接打不开，找了一个新链接，不确定是否正确）
    - [http2 explained][70]（[中译版][71]）
    - [HTTP/2 for a Faster Web][72]
    - [Nginx HTTP/2 白皮书][73]
    - [RFC 7540 - Hypertext Transfer Protocol Version 2 (HTTP/2)][74]: HTTP/2 的协议本身
    - [RFC 7541 - HPACK: Header Compression for HTTP/2][75]: HTTP/2 的压缩算法

- 网络协议词条汇集地：[Internet Protocol Suite][76]

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

  [1]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9
  [2]: https://github.com/0xAX/linux-insides
  [3]: https://lwn.net/Kernel/Index/
  [4]: https://learnlinuxconcepts.blogspot.com/2014/10/this-blog-is-to-help-those-students-and.html
  [5]: https://www.kernel.org/doc/
  [6]: https://planet.kernel.org/
  [7]: https://lenovopress.lenovo.com/redp4285.pdf
  [8]: https://tldp.org/LDP/tlk/tlk.html
  [9]: https://www.brendangregg.com/linuxperf.html
  [10]: https://dropbox.tech/infrastructure/optimizing-web-servers-for-high-throughput-and-low-latency
  [11]: https://people.freebsd.org/~lstewart/articles/cpumemory.pdf
  [12]: https://lwn.net/Articles/250967/
  [13]: https://lwn.net/Articles/252125/
  [14]: https://lwn.net/Articles/253361/
  [15]: https://lwn.net/Articles/254445/
  [16]: https://lwn.net/Articles/255364/
  [17]: https://lwn.net/Articles/256433/
  [18]: https://lwn.net/Articles/257209/
  [19]: https://lwn.net/Articles/258154/
  [20]: https://lwn.net/Articles/258188/
  [21]: http://www.puppetmastertrading.com/images/hwViewForSwHackers.pdf
  [22]: https://www.cl.cam.ac.uk/~pes20/ppc-supplemental/test7.pdf
  [23]: https://www.cl.cam.ac.uk/~pes20/weakmemory/cacm.pdf
  [24]: http://www.malloc.de/en/
  [25]: https://github.com/gperftools/gperftools
  [26]: http://jemalloc.net/
  [27]: https://people.freebsd.org/~jasone/jemalloc/bsdcan2006/jemalloc.pdf
  [28]: https://owent.net/2013/867.html
  [29]: https://blog.karatos.in/a?ID=00700-9d15fdfe-0597-46ae-b088-f3c0c3f80071
  [30]: https://engineering.fb.com/2011/01/03/core-data/scalable-memory-allocation-using-jemalloc/
  [31]: https://zapier.com/engineering/celery-python-jemalloc/
  [32]: https://book.douban.com/subject/10510747/
  [33]: https://www.site.uottawa.ca/~shervin/courses/ceg4185/lectures/
  [34]: https://www.geeksforgeeks.org/computer-network-tutorials/
  [35]: https://lartc.org/
  [36]: https://access.redhat.com/sites/default/files/attachments/20150325_network_performance_tuning.pdf
  [37]: https://github.com/caesar0301/awesome-pcaptools
  [38]: https://legacy.netdevconf.info/1.2/papers/bbr-netdev-1.2.new.new.pdf
  [39]: https://blog.packagecloud.io/monitoring-tuning-linux-networking-stack-receiving-data/
  [40]: https://blog.packagecloud.io/monitoring-tuning-linux-networking-stack-sending-data/
  [41]: https://www.rfc-editor.org/rfc/rfc826
  [42]: https://www.rfc-editor.org/rfc/rfc1853
  [43]: https://www.rfc-editor.org/rfc/rfc2784
  [44]: https://www.rfc-editor.org/rfc/rfc2661
  [45]: https://www.rfc-editor.org/rfc/rfc2637
  [46]: https://coolshell.cn/articles/11564.html
  [47]: https://coolshell.cn/articles/11609.html
  [48]: https://www.rfc-editor.org/rfc/rfc793
  [49]: https://www.rfc-editor.org/rfc/rfc813
  [50]: https://www.rfc-editor.org/rfc/rfc879
  [51]: https://www.rfc-editor.org/rfc/rfc896
  [52]: https://www.rfc-editor.org/rfc/rfc2581
  [53]: https://www.rfc-editor.org/rfc/rfc5681
  [54]: https://www.rfc-editor.org/rfc/rfc6582
  [55]: https://www.rfc-editor.org/rfc/rfc2018
  [56]: https://www.rfc-editor.org/rfc/rfc2883
  [57]: https://www.rfc-editor.org/rfc/rfc2988
  [58]: https://www.rfc-editor.org/rfc/rfc6298
  [59]: https://ee.lbl.gov/papers/congavoid.pdf
  [60]: https://man7.org/linux/man-pages/man7/tcp.7.html
  [61]: https://book.douban.com/subject/10746113/
  [62]: https://www.rfc-editor.org/rfc/rfc2616
  [63]: https://tools.ietf.org/html/rfc7230
  [64]: https://www.rfc-editor.org/rfc/rfc7231
  [65]: https://www.rfc-editor.org/rfc/rfc7232
  [66]: https://www.rfc-editor.org/rfc/rfc7233
  [67]: https://www.rfc-editor.org/rfc/rfc7235
  [68]: https://en.wikipedia.org/wiki/HTTP/2
  [69]: https://github.com/jiajunhuang/http2-illustrated
  [70]: https://daniel.haxx.se/http2/
  [71]: https://http2-explained.haxx.se/zh
  [72]: https://cascadingmedia.com/insites/2015/03/http-2.html
  [73]: https://www.nginx.com/wp-content/uploads/2015/09/NGINX_HTTP2_White_Paper_v4.pdf
  [74]: https://httpwg.org/specs/rfc7540.html
  [75]: https://httpwg.org/specs/rfc7541.html
  [76]: https://en.wikipedia.org/wiki/Internet_protocol_suite

# 《程序员练级攻略》分析笔记

## 第9章 异步 I/O 模型和 Lock-Free 编程

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- 异步 I/O 模型
- Lock-Free 编程
- 系统底层其他知识
- 相关论文

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 异步 I/O 模型

- 异步 I/O 模型的重要性
  - 异步 I/O 模型是我个人觉得所有程序员都必需要学习的一门技术或是编程方法，这其中的设计模式或是解决方法可以借鉴到分布式架构上来。

- 史蒂文斯（Stevens）在《UNIX 网络编程》一书 6.2 I/O Models 中介绍了五种 I/O 模型
  - 阻塞 I/O
  - 非阻塞 I/O
  - I/O 的多路复用（select 和 poll）
  - 信号驱动的 I/O（SIGIO）
  - 异步 I/O（POSIX 的 aio_functions）

- [C10K Problem][1]

- [Thousands of Threads and Blocking I/O: The Old Way to Write Java Servers Is New Again (and Way Better)][2]
  - 一篇和 Java 相关的 I/O 模型的文章来复习一下之前的内容。
  - 这个 PPT 中不仅回顾和比较了各种 I/O 模型，而且还有各种比较细节的方案和说明，是一篇非常不错的文章。

- [Scalable IO in Java][3]
  - Java 相关的 PPT

- 各种异步 I/O 的实现和设计方式
  - [IBM - Boost application performance using asynchronous I/O][4]: 这是一篇关于 AIO 的文章。
  - [Lazy Asynchronous I/O For Event-Driven Servers][5]: 这篇文章也很不错。
  - 另外，异步 I/O 模型中的 [Windows I/O Completion Ports][6], 你也需要了解一下。
    - 如果 MSDN 上的这个手册不容易读，你可以看看这篇文章 [Inside I/O Completion Ports][7]。
    - 另外，关于 Windows，[Windows Internals][8] 这本书你可以仔细读一下，非常不错的。
    - 其中有一节 I/O Processing 也是很不错的，这里我给一个网上免费的链接 [I/O Processing][9]，你可以看看 Windows 是怎么玩的。
  - Libevent
    - 你可以看一下其主要维护人员尼克·马修森（Nick Mathewson）写的 [Libevent 2.0 book][10]
    - 还有一本国人写的电子书[《Libevent 深入浅出》][11]。
  - Libuv。你可以看一下其官网的 [Libuv Design Overview][12] 了解一下。

- 简单总结
  - 异步 I/O 模型的发展技术是： select -> poll -> epoll -> aio -> libevent -> libuv。
  - Unix/Linux 用了好几十年走过这些技术的变迁，然而，都不如 Windows I/O Completion Port 设计得好。（个人观点）
  - 看过这些各种异步 I/O 模式的实现以后，相信你会看到一个编程模式——Reactor 模式。

- Reactor 模式（读以下三篇就够了）
  - [Understanding Reactor Pattern: Thread-Based and Event-Driven][13]
  - [Reactor Pattern][14]
  - [The reactor pattern and non-blocking IO][15] （不确定链接是否正确）

- C10M Problem: [The Secret To 10 Million Concurrent Connections -The Kernel Is The Problem, Not The Solution][16]

- 还有几篇可能有争议的文章，让你从不同的角度思考。
  - [Select is fundamentally broken][17]
  - [Epoll is fundamentally broken 1/2][18]
  - [Epoll is fundamentally broken 2/2][19]

#### Lock-Free 编程

- 关于无锁的数据结构的几篇教程
  - [Dr.Dobb’s: Lock-Free Data Structures][20]
  - [Andrei Alexandrescu: Lock-Free Data Structures][21]

- 并行编程的经典书（强烈推荐）
  - [Is Parallel Programming Hard, And, If So, What Can You Do About It?][22]

- Wikipedia 关于并发编程的三个词条
  - [Non-blocking algorithm][23]
  - [Read-copy-update][24]
  - [Seqlock][25]

- 两篇论文
  - [Implementing Lock-Free Queues][26]
    - 这也是一篇很不错的论文，我把它介绍在了我的网站上，文章为 [无锁队列的实现][27]。
    - [Simple, Fast, and Practical Non-Blocking and Blocking Concurrent Queue Algorithms][28]: 这篇论文给出了一个无阻塞和阻塞的并发队列算法。

- 几个博客
  - [1024cores][29]: 德米特里·伐由科夫（Dmitry Vyukov）的和 lock-free 编程相关的网站。
  - [Paul E. McKenney][30]: 保罗（Paul）的个人网站。
  - [Concurrency Freaks][31]: 关于并发算法和相关模式的网站。
  - [Preshing on Programming][32]: 加拿大程序员杰夫·普莱辛（Jeff Preshing）的技术博客，主要关注 C++ 和 Python 两门编程语言。
    - 他用 C++11 实现了类的反射机制，用 C++ 编写了 3D 小游戏 Hop Out，还为该游戏编写了一个游戏引擎。
    - 他还讨论了很多 C++ 的用法，比如 C++14 推荐的代码写法、新增的某些语言构造等，和 Python 很相似。
    - 阅读这个技术博客上的内容能够深深感受到博主对编程世界的崇敬和痴迷。
  - [Sutter’s Mill][33]: 赫布·萨特（Herb Sutter）是一位杰出的 C++ 专家，曾担任 ISO C++ 标准委员会秘书和召集人超过 10 年。
    - 他的博客有关于 C++ 语言标准最新进展的信息，其中也有他的演讲视频。
    - 博客中还讨论了其他技术和 C++ 的差异，如 C# 和 JavaScript，它们的性能特点、怎样避免引入性能方面的缺陷等。
  - [Mechanical Sympathy][34]: 博主是马丁·汤普森（Martin Thompson），他是一名英国的技术极客，探索现代硬件的功能，并提供开发、培训、性能调优和咨询服务。
    - 他的博客主题是 Hardware and software working together in harmony，里面探讨了如何设计和编写软件使得它在硬件上能高性能地运行。非常值得一看。

- 一些 C/C++ 的类库（对于 Java 的，请参看 JDK 里的 Concurrent 开头的一系列的类）
  - [Boost.Lockfree][35]: Boost 库中的无锁数据结构。
  - [ConcurrencyKit][36]: 并发性编程的原语。
  - [Folly][37]: Facebook 的开源库（它对 MPMC 队列做了一个很好的实现）。
  - [Junction][38]: C++ 中的并发数据结构。
  - [MPMCQueue][39]: 一个用 C++11 编写的有边界的“多生产者 - 多消费者”无锁队列。
  - [SPSCQueue][40]: 一个有边界的“单生产者 - 单消费者”的无等待、无锁的队列。
  - [Seqlock][41]: 用 C++ 实现的 Seqlock。
  - [Userspace RCU][42]: liburcu 是一个用户空间的 RCU（Read-copy-update，读 - 拷贝 - 更新）库。
  - [libcds][43]: 一个并发数据结构的 C++ 库。liblfds - 一个用 C 语言编写的可移植、无许可证、无锁的数据结构库。

#### 系统底层其他知识

- [All about 64-bit programming in one place][44]
  - 这是一个关于 64 位编程相关的收集页面，其中包括相关的文章、28 节课程，还有知识库和相关的 blog。
  - 关于 64 位系统编程，只要去这个地方就行了。

- [What Scalable Programs Need from Transactional Memory][45]
  - 事务性内存（TM）一直是许多研究的重点，它在诸如 IBM Blue Gene/Q 和 Intel Haswell 等处理器中得到了支持。
  - 许多研究都使用 STAMP 基准测试套件来评估其设计。然而，我们所知的所有 TM 系统上的 STAMP 基准测试所获得的加速比较有限。
  - 例如，在 IBM Blue Gene/Q 上有 64 个线程，我们观察到使用 Blue Gene/Q 硬件事务内存（HTM）的中值加速比为 1.4 倍，使用软件事务内存（STM）的中值加速比为 4.1 倍。
  - 什么限制了这些 TM 基准的性能？
  - 在本论文中，作者认为问题在于用于编写它们的编程模型和数据结构上，只要使用合适的模型和数据结构，程序的性能可以有 10 多倍的提升。

- [Improving OpenSSL Performance][46]: 这篇文章除了教你如何提高 OpenSSL 的执行性能，还讲了一些底层的性能调优知识。

- 关于压缩的内容
  - [How eBay’s Shopping Cart used compression techniques to solve network I/O bottlenecks][47]
    - 这是一篇很好的文章，讲述了 eBay 是如何通过压缩数据来提高整体服务性能的，其中有几个比较好的压缩算法。
    - 除了可以让你学到相关的技术知识，还可以让你看到一种比较严谨的工程师文化。
  - [Linkedin: Boosting Site Speed Using Brotli Compression][48]
    - LinkedIn 在 2017 年早些时候开始使用 [Brotli][49] 来替换 gzip，以此带来更快的访问
    - 这篇文章讲述了什么是 Brotli 以及与其它压缩程序的比较和所带来的性能提升。

- Linux/Unix 安全编程
  - [Secure Programming HOWTO - Creating Secure Software][50]

#### 相关论文

- [Hints for Computer System Design][51]
  - 计算机设计的忠告，这是 ACM 图灵奖得主 Butler Lampson 在 Xerox PARC 工作时的一篇论文。
  - 这篇论文简明扼要地总结了他在做系统设计时的一些想法，非常值得一读。

- 5 分钟法则和 5 字节法则
  - [The 5 minute rule for trading memory for disc accesses and the 5 byte rule for trading memory for CPU time][52]
  - [The Five-Minute Rule Ten Years Later and Other Computer Storage Rules of Thumb][53]: 10年后对该法则的重新审视
  - [The Five-Minute Rule 20 Years Later (and How Falsh Memory Changes the Rules][54]

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

  [1]: https://en.wikipedia.org/wiki/C10k_problem
  [2]: https://www.slideshare.net/e456/tyma-paulmultithreaded1
  [3]: http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf
  [4]: https://developer.ibm.com/articles/l-async/
  [5]: https://www.usenix.org/legacy/event/usenix04/tech/general/full_papers/elmeleegy/elmeleegy_html/html.html
  [6]: https://learn.microsoft.com/en-us/windows/win32/fileio/i-o-completion-ports
  [7]: https://web.archive.org/web/20101031075704/http://doc.sch130.nsc.ru/www.sysinternals.com/ntw2k/info/comport.shtml
  [8]: https://book.douban.com/subject/6935552/
  [9]: https://flylib.com/books/en/4.491.1.85/1/
  [10]: http://www.wangafu.net/~nickm/libevent-book/
  [11]: https://aceld.gitbooks.io/libevent/content/
  [12]: http://docs.libuv.org/en/v1.x/design.html
  [13]: https://dzone.com/articles/understanding-reactor-pattern-thread-based-and-eve
  [14]: https://www.dre.vanderbilt.edu/~schmidt/PDF/Reactor2-93.pdf
  [15]: https://www.cnblogs.com/davidwang456/p/3705780.html
  [16]: http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html
  [17]: https://idea.popcount.org/2017-01-06-select-is-fundamentally-broken/
  [18]: https://idea.popcount.org/2017-02-20-epoll-is-fundamentally-broken-12/
  [19]: https://idea.popcount.org/2017-03-20-epoll-is-fundamentally-broken-22/
  [20]: https://www.drdobbs.com/lock-free-data-structures/184401865
  [21]: http://erdani.org/publications/cuj-2004-10.pdf
  [22]: https://mirrors.edge.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html
  [23]: https://en.wikipedia.org/wiki/Non-blocking_algorithm
  [24]: https://en.wikipedia.org/wiki/Read-copy-update
  [25]: https://en.wikipedia.org/wiki/Seqlock
  [26]: https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.53.8674&rep=rep1&type=pdf
  [27]: https://coolshell.cn/articles/8239.html
  [28]: https://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf
  [29]: https://www.1024cores.net/
  [30]: http://paulmck.livejournal.com/
  [31]: http://concurrencyfreaks.blogspot.com/
  [32]: https://preshing.com/
  [33]: https://herbsutter.com/
  [34]: https://mechanical-sympathy.blogspot.com/
  [35]: https://www.boost.org/doc/libs/1_60_0/doc/html/lockfree.html
  [36]: https://github.com/concurrencykit/ck
  [37]: https://github.com/facebook/folly
  [38]: https://github.com/preshing/junction
  [39]: https://github.com/rigtorp/MPMCQueue
  [40]: https://github.com/rigtorp/SPSCQueue
  [41]: http://liburcu.org/
  [42]: https://github.com/khizmax/libcds
  [43]: https://liblfds.org/
  [44]: https://www.intel.com/content/www/us/en/developer/topic-technology/data-center/overview.html
  [45]: https://dl.acm.org/doi/10.1145/3037697.3037750
  [46]: https://www.intel.com/content/www/us/en/developer/topic-technology/client/business.html
  [47]: https://tech.ebayinc.com/engineering/how-ebays-shopping-cart-used-compression-techniques-to-solve-network-io-bottlenecks/
  [48]: https://engineering.linkedin.com/blog/2017/05/boosting-site-speed-using-brotli-compression
  [49]: https://en.wikipedia.org/wiki/Brotli
  [50]: https://dwheeler.com/secure-programs/
  [51]: https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/acrobat-17.pdf
  [52]: http://www.hpl.hp.com/techreports/tandem/TR-86.1.pdf
  [53]: http://jimgray.azurewebsites.net/5_min_rule_sigmod.pdf
  [54]: https://cacm.acm.org/magazines/2009/7/32091-the-five-minute-rule-20-years-later/fulltext

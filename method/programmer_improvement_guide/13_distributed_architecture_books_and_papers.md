# 《程序员练级攻略》分析笔记

## 第13章 分布式架构经典图书和论文

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- 经典图书
- 经典论文
  - 分布式事务
  - Paxos 一致性算法
  - Raft 一致性算法
  - Gossip 一致性算法
  - 分布式存储和数据库
  - 分布式消息系统
  - 日志和数据
  - 分布式监控和跟踪
  - 数据分析
  - 与编程相关的论文
  - 其他的分布式论文阅读列表

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 经典图书

- [Distributed Systems for fun and profit][1]
  - 这是一本免费的电子书。
  - 作者撰写此书的目的是希望以一种更易于理解的方式，讲述以亚马逊的 Dynamo、谷歌的 Bigtable 和 MapReduce 等为代表的分布式系统背后的核心思想。

- [Designing Data Intensive Application][2]
  - 这本书是一本非常好的书，这本书深入浅出地用很多的工程案例讲解了如何让数据结点做扩展。
  - 作者马丁·科勒普曼（Martin Kleppmann）完整地梳理各类纷繁复杂设计背后的技术逻辑，不同架构之间的妥协与超越，很值得开发人员与架构设计者阅读。

- [Distributed Systems: Principles and Paradigms][3]
  - 由计算机科学家安德鲁·斯图尔特·塔能鲍姆（Andrew S. Tanenbaum）和其同事马丁·范·斯蒂恩（Martin van Steen）合力撰写的，是分布式系统方面的经典教材。
  - 本书不是一本指导“如何做”的手册，仅适合系统性地学习基础知识，了解编写分布式系统的基本原则和逻辑。
  - 中文版：[《分布式系统原理与范型》（第二版）][4]。

- [Scalable Web Architecture and Distributed System][5]
  - 这是一本免费的在线小册子，其中文翻译版为 [可扩展的 Web 架构和分布式系统][6]。
  - 本书从大型互联网系统的常见特性，如高可用、高性能、高可靠、易管理等出发，引出了一个类似于 Flickr 的典型的大型图片网站的例子。

- [Principles of Distributed Systems][66]
  - 本书是苏黎世联邦理工学院的教材。它讲述了多种分布式系统中会用到的算法。

#### 经典论文

##### 分布式事务

- [《Transaction Across DataCenter》][7]（[YouTube 视频][8]）。
  - Google App Engine 联合创始人瑞恩·巴雷特（Ryan Barrett）在 2009 年的 Google I/O 大会上的演讲

- [《分布式系统的事务处理》][9]：酷壳上的一篇文章。

##### Paxos 一致性算法

- Paxos 算法简介
  - Paxos 算法，是莱斯利·兰伯特（Lesile Lamport）于 1990 年提出来的一种基于消息传递且具有高度容错特性的一致性算法。
  - 但是这个算法太过于晦涩，所以一直以来都属于理论上的论文性质的东西。
  - 其真正进入工程圈，主要是来源于 Google 的 Chubby lock——一个分布式的锁服务，用在了 Bigtable 中。

- Google 发布的两篇与 Paxos 相关的论文
  - [Bigtable: A Distributed Storage System for Structured Data][10]
  - [The Chubby lock service for loosely-coupled distributed systems][11]

- Google 与 Bigtable 相齐名的还有另外两篇论文。
  - [The Google File System][12]
  - [MapReduce: Simplified Data Processing on Large Clusters][13]

- Paxos 工程实现细节
  - [Paxos Made Live - An Engineering Perspective][14]

- Paxos 算法的两篇通俗易懂的文章
  - [Neat Algorithms - Paxos][15]
  - [Paxos by Examples][16]

##### Raft 一致性算法

- Raft 原始论文
  - [In search of an Understandable Consensus Algorithm (Extended Version)][17]
  - [《Raft 一致性算法论文译文》][18]

- Raft 算法的动画演示
  - [Raft - The Secret Lives of Data][19]
  - [Raft Consensus Algorithm][20]
  - [Raft Distributed Consensus Algorithm Visualization][21]

##### Gossip 一致性算法

- [Dynamo: Amazon’s Highly Available Key Value Store][22]
  - Amazon 的 DynamoDB
  - 这篇文章中有几个关键的概念，一个是 Vector Clock，另一个是 Gossip 协议。

- Vector Clock
  - [Time, Clocks and the Ordering of Events in a Distributed System][23]：被誉为第一篇真正的“分布式系统”论文。
  - [马萨诸塞大学课程 Distributed Operating System][24] 中第 10 节 [Clock Synchronization][67]：这篇讲义讲述了时钟同步的问题。
  - [Why Vector Clocks are Easy][25]
  - [Why Vector Clocks are Hard][26]

- Gossip 协议原始论文
  - [Efficient Reconciliation and Flow Control for Anti-Entropy Protocols][27]

- Gossip 视频介绍
  - [Understanding Gossip (Cassandra Internals)][28]

- Gossip 动画
  - [Gossip Visualization][29]

##### 分布式存储和数据库

- Amazon Aurora
  - [Design Considerations for High Throughput Cloud -Native Relation Databases][30]

- Google Spanner
  - [Google’s Globally-Distributed Database][31]
  - [Spanner, TrueTime & The CAP Theorem][32]： 2017 年的新版论文

- [F1 - The Fault-Tolerant Distributed RDBMS Supporting Google’s Ad Business][33]

- [Cassandra: A Decentralized Structured Storage System ][34]

- CRUSH 和 Ceph
  - [CRUSH: Controlled, Scalable, Decentralized Placement of Replicated Data][35]：这里提到的算法被应用在了 Ceph 分布式文件系统中
  - [RADOS - A Scalable, Reliable Storage Service for Petabyte-scale Storage Clusters][36]：Ceph 的架构
  - [Ceph 的架构文档][37]

##### 分布式消息系统

- [Kafka: a Distributed Messaging System for Log Processing][38]
  - 分布式消息系统必读

- [Wormhole: Reliable Pub-Sub to Support Geo-replicated Internet Services][39]
  - Wormhole 是 Facebook 内部使用的一个 Pub-Sub 系统，目前还没有开源。

- [All Aboard the Databus! LinkedIn’s Scalable Consistent Change Data Capture Platform][40]
  - 指出支持对不同数据源的抽取，允许不同数据源抽取器的开发和接入，只需该抽取器遵循设计规范即可。
  - 该规范的一个重要方面就是每个数据变化都必须被一个单调递增的数字标注（SCN），用于同步。
  - 这其中的一些方法完全可以用做异地双活的系统架构中。
  - [相关 PPT 分享][42]

##### 日志和数据

- [The Log: What every software engineer should know about real-time data’s unifying abstraction][43]:
  - 这篇文章好长，不过这是一篇非常好非常好的文章，这是每个工程师都应该知道的事，必看。
  - [《日志：每个软件工程师都应该知道的有关实时数据的统一概念》][44]：中译版。

- [The Log-Structured Merge-Tree (LSM-Tree)][45]
  - 多年前，谷歌发表了 Bigtable 的论文，论文中很多很酷的方面，其一就是它所使用的文件组织方式，这个方法更一般的名字叫 Log Structured-Merge Tree。
  - LSM 是当前被用在许多产品的文件结构策略：HBase、Cassandra、LevelDB、SQLite，甚至在 MongoDB 3.0 中也带了一个可选的 LSM 引擎（Wired Tiger 实现的）。
  - LSM 有趣的地方是它抛弃了大多数数据库所使用的传统文件组织方法。实际上，当你第一次看它时是违反直觉的。这篇论文可以让你明白这个技术。
  - 参考阅读中文社区里的这几篇文章：[文章一][46]、[文章二][47]。）

- [Immutability Changes Everything][48]
  - 这篇论文是现任 Salesforce 软件架构师帕特·赫兰德（Pat Helland）在 CIDR 2015 大会上发表的。
  - [相关视频演讲][49]

- [Tango: Distributed Data Structures over a Shared Log][50]
  - 这个论文非常经典，其中说明了不可变性（immutability）架构设计的优点。

##### 分布式监控和跟踪

- [Dapper, a Large-Scale Distributed Systems Tracing Infrastructur][51]
  - Google 的分布式跟踪监控论文。
  - 其开源实现有三个：[Zipkin][52]、[Pinpoint][53] 和 [HTrace][54]。我个人更喜欢 Zipkin。

##### 数据分析

- [The Unified Logging Infrastructure for Data Analytics at Twitter][55]
  - Twitter 公司的一篇关于日志架构和数据分析的论文。

- [Scaling Big Data Mining Infrastructure: The Twitter Experience][56]
  - 讲 Twitter 公司的数据分析平台在数据量越来越大，架构越来越复杂，业务需求越来越多的情况下，数据分析从头到底是怎么做的。

- [Dremel: Interactive Analysis of Web-Scale Dataset][57]
  - Google 公司的 Dremel，是一个针对临时查询提供服务的系统，它处理的是只读的多层数据。
  - 本篇文章介绍了它的架构与实现，以及它与 MapReduce 是如何互补的。

- [Resident Distributed Datasets: a Fault-Tolerant Abstraction for In-Memory Cluster Computin][58]
  - 这篇论文提出了弹性分布式数据集（Resilient Distributed Dataset，RDD）的概念。

##### 与编程相关的论文

- [Distributed Programming Model][59]
- [PSync: a partially synchronous language for fault-tolerant distributed algorithms][60]
- [Programming Models for Distributed Computing][61]
- [Logic and Lattices for Distributed Programming][62]

##### 其他的分布式论文阅读列表

- [Services Engineering Reading List][63]
- [Readings in Distributed Systems][64]
- [Google Research - Distributed Systems and Parallel Computing][65]

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

  [1]: http://book.mixu.net/distsys/single-page.html
  [2]: https://book.douban.com/subject/27154352/
  [3]: http://barbie.uta.edu/~jli/Resources/MapReduce&Hadoop/Distributed%20Systems%20Principles%20and%20Paradigms.pdf
  [4]: https://book.douban.com/subject/3108801/
  [5]: http://www.aosabook.org/en/distsys.html
  [6]: http://nettee.github.io/posts/2016/Scalable-Web-Architecture-and-Distributed-Systems/
  [7]: https://snarfed.org/transactions_across_datacenters_io.html
  [8]: https://www.youtube.com/watch?v=srOgpXECblk
  [9]: https://coolshell.cn/articles/10910.html
  [10]: https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf
  [11]: https://static.googleusercontent.com/media/research.google.com/en//archive/chubby-osdi06.pdf
  [12]: https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf
  [13]: https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf
  [14]: https://static.googleusercontent.com/media/research.google.com/en//archive/paxos_made_live.pdf
  [15]: http://harry.me/blog/2014/12/27/neat-algorithms-paxos/
  [16]: https://angus.nyc/
  [17]: https://raft.github.io/raft.pdf
  [18]: https://www.infoq.cn/article/raft-paper
  [19]: http://thesecretlivesofdata.com/raft/
  [20]: https://raft.github.io/
  [21]: http://kanaka.github.io/raft.js/
  [22]: https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf
  [23]: https://www.microsoft.com/en-us/research/publication/time-clocks-ordering-events-distributed-system/
  [24]: https://lass.cs.umass.edu/~shenoy/courses/spring05/lectures.html
  [25]: https://riak.com/why-vector-clocks-are-easy/
  [26]: https://riak.com/posts/technical/why-vector-clocks-are-hard/
  [27]: https://www.cs.cornell.edu/home/rvr/papers/flowgossip.pdf
  [28]: https://www.youtube.com/watch?v=FuP1Fvrv6ZQ
  [29]: https://rrmoelker.github.io/gossip-visualization/
  [30]: https://pdos.csail.mit.edu/6.824/papers/aurora.pdf
  [31]: http://static.googleusercontent.com/media/research.google.com/zh-CN//archive/spanner-osdi2012.pdf
  [32]: https://static.googleusercontent.com/media/research.google.com/zh-CN//pubs/archive/45855.pdf
  [33]: http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/38125.pdf
  [34]: https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.161.6751&rep=rep1&type=pdf
  [35]: https://www.ssrc.us/Papers/weil-sc06.pdf
  [36]: https://ceph.com/assets/pdfs/weil-rados-pdsw07.pdf
  [37]: https://docs.ceph.com/en/latest/architecture/
  [38]: http://notes.stephenholiday.com/Kafka.pdf
  [39]: https://www.usenix.org/system/files/conference/nsdi15/nsdi15-paper-sharma.pdf
  [40]: https://engineering.linkedin.com/research/2012/all-aboard-the-databus-linkedlns-scalable-consistent-change-data-capture-platform
  [42]: https://www.slideshare.net/amywtang/databus-socc-v3
  [43]: https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying
  [44]: https://github.com/oldratlee/translations/blob/master/log-what-every-software-engineer-should-know-about-real-time-datas-unifying/README.md
  [45]: https://www.cs.umb.edu/~poneil/lsmtree.pdf
  [46]: https://www.cnblogs.com/siegfang/archive/2013/01/12/lsm-tree.html
  [47]: https://kernelmaker.github.io/lsm-tree
  [48]: https://www.cidrdb.org/cidr2015/Papers/CIDR15_Paper16.pdf
  [49]: https://vimeo.com/52831373
  [50]: https://www.microsoft.com/en-us/research/wp-content/uploads/2013/11/Tango.pdf
  [51]: http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf
  [52]: https://zipkin.io/
  [53]: https://github.com/pinpoint-apm/pinpoint
  [54]: https://incubator.apache.org/projects/htrace.html
  [55]: http://vldb.org/pvldb/vol5/p1771_georgelee_vldb2012.pdf
  [56]: http://www.datascienceassn.org/sites/default/files/Scaling%20Big%20Data%20Mining%20Infrastructure%20-%20The%20Twitter%20Experience.pdf
  [57]: http://static.googleusercontent.com/media/research.google.com/en/us/pubs/archive/36632.pdf
  [58]: https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final138.pdf
  [59]: https://web.cs.ucdavis.edu/~pandey/Research/Papers/icdcs01.pdf
  [60]: https://www.di.ens.fr/~cezarad/popl16.pdf
  [61]: https://heather.miller.am/teaching/cs7680/
  [62]: https://dsf.berkeley.edu/papers/UCB-lattice-tr.pdf
  [63]: https://github.com/mmcgrana/services-engineering
  [64]: http://christophermeiklejohn.com/distributed/systems/2013/07/12/readings-in-distributed-systems.html
  [65]: https://research.google/pubs/
  [66]: https://disco.ethz.ch/courses/podc_allstars/lecture/podc.pdf
  [67]: https://lass.cs.umass.edu/~shenoy/courses/spring05/lectures/Lec10.pdf

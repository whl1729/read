# 《程序员练级攻略》分析笔记

## 第14章 分布式架构工程设计

### Q1：这一章的内容属于哪一类别？

计算机/方法论。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- 分布式架构设计原则
- 分布式架构设计模式
- 分布式架构设计与工程实践
  - 分布式系统的故障测试
  - 弹性伸缩
  - 一致性哈希
  - 数据库分布式
  - 缓存
  - 消息队列
  - 日志
  - 性能
  - 搜索
  - 各公司的架构实践

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 分布式架构设计原则

- [Designs, Lessons and Advice from Building Large Distributed System][1]
  - Google 杰夫·迪恩（Jeff Dean）2009 年一次演讲的 PPT。

- [Building Software Systems At Google and Lessons Learned][2]
  - 2010 年，斯坦福大学请杰夫·迪恩到大学里给他们讲了一节课，回顾了 Google 发展的历史。

- [The Twelve-Factor App ][3]（[中文版][4]）
  - 如今，软件通常会作为一种服务来交付，它们被称为网络应用程序，或软件即服务（SaaS）。
  - 12-Factor 为构建 SaaS 应用提供了方法论，是架构师必读的文章。

- [Notes on Distributed Systems for Young Bloods][5]
  - 给准备进入分布式系统领域的人的一些忠告。

- [On Designing and Deploying Internet-Scale Services][6]（[中译版][7]）
  - 微软 Windows Live 服务平台的一些经验性的总结文章，很值得一读。

- [4 Things to Keep in Mind When Building a Platform for the Enterprise][8] （链接无效了）
  - Box 平台 VP 海蒂·威廉姆斯（Heidi Williams）撰写的一篇文章，阐述了为企业构建平台时需要牢记的四件关于软件设计方面的事：
    1. Design Broadly, Build Narrowly.
    2. Platforms Are Powerful and Flexible. Choose wisely what to expose when!
    3. Build Incrementally, Get Feedback, and Iterate.
    4. Create a Platform-first Mentality.

- [Principles of Chaos Engineering][9]
  - 我们知道，Netflix 公司有一个叫 Chaos Monkey 的东西，这个东西会到分布式系统里“瞎搞”，以此来测试系统的健壮和稳定性。
  - 这个视频中，Netflix 分享了一些软件架构的经验和原则，值得一看。

- [Building Fast & Resilient Web Applications][10]
  - 伊利亚·格里高利克（Ilya Grigorik）在 Google I/O 2016 上的一次关于如何通过弹力设计来实现快速和可容错的网站架构的演讲，其中有好些经验分享。

- [Design for Resiliency][12]
  - 这篇文章带我们全面认识“弹力（Resiliency）”，以及弹力对于系统的重要性，并详细阐述了如何设计和实现系统的弹力。

- 微软的 Azure 网站上有一系列的 [Design Principle][13] 的文章，你可以看看这几篇：
  - [Design for Self-healing][112]
  - [Design for Scaling Out][113]
  - [Design for Evolution][114]

- [Eventually Consistent][14]
  - AWS CTO 维尔纳·沃格尔斯（Werner Vogels）发布在自己 Blog 上的一篇关于最终一致性的好文。

- [Writing Code that Scales][15]
  - Rackspace 的一篇很不错的博文，告诉我们一些很不错的写出高扩展和高性能代码的工程原则。

- [Automate and Abstract: Lessons from Facebook on Engineering for Scale][16]
  - 软件自动化和软件抽象，这是软件工程中最重要的两件事了。
  - 通过这篇文章，我们可以看到 Facebook 的关于这方面的一些经验教训。

#### 分布式架构设计模式

- 微软云平台 Azure 上的设计模式：[Cloud Design Patterns][17]
  - [设计模式：可用性][18]
  - [设计模式：数据管理][19]
  - [设计模式：设计和实现][20]
  - [设计模式：消息][21]
  - [设计模式：管理和监控][22]
  - [设计模式：性能和扩展][23]
  - [设计模式：系统弹力][24]
  - [设计模式：安全][25]

- 其它一些关于分布式系统设计模式的网站和相关资料
  - [AWS Cloud Pattern][26]
    - 这里收集了 AWS 云平台的一些设计模式。
  - [Design patterns for container-based distributed systems][27]
    - 这是 Google 给的一篇论文，其中描述了容器化下的分布式架构的设计模式。
  - [Patterns for distributed systems][28]
    - 这是一个 PPT，其中讲了一些分布式系统的架构模式，你可以顺着到 Google 里去搜索。

- 各种各样的服务架构模式
  - [A Pattern Language for Micro-Services][29]
  - [SOA Patterns][30]

- 陈皓对分布式设计模式的总结
  - 弹力设计篇，内容包括：认识故障和弹力设计、隔离设计、异步通讯设计、幂等性设计、服务的状态、补偿事务、重试设计、熔断设计、限流设计、降级设计、弹力设计总结。
  - 管理设计篇，内容包括：分布式锁、配置中心、边车模式、服务网格、网关模式、部署升级策略等。
  - 性能设计篇，内容包括：缓存、异步处理、数据库扩展、秒杀、边缘计算等。

#### 分布式架构设计与工程实践

##### 分布式系统的故障测试

- [FIT: Failure Injection Testing][31]
  - Netflix 公司的一篇关于做故障注入测试的文章。

- [Automated Failure Testing][32]
  - 同样来自 Netflix 公司的自动化故障测试的一篇博文。

- [Automating Failure Testing Research at Internet Scale][33]
  - Netflix 公司伙同圣克鲁斯加利福尼亚大学和 Gremlin 游戏公司一同撰写的一篇论文。

##### 弹性伸缩

- [4 Architecture Issues When Scaling Web Applications: Bottlenecks, Database, CPU, IO][34]
  - 讲解了后端程序的主要性能指标，即响应时间和可伸缩性这两者如何能提高的解决方案。
  - 讨论了包括纵向和横向扩展，可伸缩架构、负载均衡、数据库的伸缩、CPU 密集型和 I/O 密集型程序的考量等。

- [Scaling Stateful Objects][35]
  - 这是一本叫《Development&Deployment of Multiplayer Online Games》书中一章内容的节选，讨论了有状态和无状态的节点如何伸缩的问题。
  - 虽然还没有写完，但是可以给你一些很不错的基本概念和想法。

- [Scale Up vs Scale Out: Hidden Costs][36]
  - Coding Horror 上的一篇有趣的文章，详细分析了可伸缩性架构的不同扩展方案（横向扩展或纵向扩展）所带来的成本差异，帮助你更好地选择合理的扩展方案，可以看看。

- [Best Practices for Scaling Out][37]
  - OpenShift 的一篇讨论 Scale out 最佳实践的文章。

- [Scalability Worst Practices][38]
  - 这篇文章讨论了一些最差实践，你需要小心避免。

- [Reddit: Lessons Learned From Mistakes Made Scaling To 1 Billion Pageviews A Month][39]
  - Reddit 分享的一些关于系统扩展的经验教训。

- 几篇关于自动化弹性伸缩的文章
  - [Autoscaling Pinterest][40]
  - [Square: Autoscaling Based on Request Queuing][41]
  - [PayPal: Autoscaling Applications][42]
  - [Trivago: Your Definite Guide For Autoscaling Jenkins][43]
  - [Scryer: Netflix’s Predictive Auto Scaling Engine。][44]

##### 一致性哈希

- [Consistent Hashing][45]
  - 这是一个一致性哈希的简单教程，其中还有代码示例。

- [Consistent Hashing: Algorithmic Tradeoffs][46]
  - 这篇文章讲述了一致性哈希的一些缺陷和坑，以及各种哈希算法的性能比较，最后还给了一组代码仓库，其中有各种哈希算法的实现。

- [Distributing Content to Open Connect][47]
  - Netflix 的一个对一致性哈希的实践，提出了 Uniform Consistent Hashing，是挺有意思的一篇文章。

- [Consistent Hashing in Cassandra][48]
  - 这是 Cassandra 中使用到的一致性哈希的相关设计。

##### 数据库分布式

- [Life Beyond Distributed Transactions][49]
  - 该文是 Salesforce 的软件架构师帕特·赫兰德（Pat Helland）于 2016 年 12 月发表的针对其在 2007 年 CIDR（创新数据库研究会议）上首次发表的同名文章的更新和缩写版本。
  - 赫兰德文中提出了重要的观点：“如果你不能使用分布式事务，那么你就只能使用工作流。”

- [How Sharding Works][50]
  - 这是一篇很不错的探讨数据 Sharding 的文章。
  - 基本上来说，数据 Sharding 可能的问题都在这篇文章里谈到了。

- [Why you don’t want to shard][51]
  - 这是 Percona 的一篇文章，其中表达了，不到万不得已不要做数据库分片。
  - 是的，最好还是先按业务来拆分，先把做成微服务的架构，然后把数据集变简单，然后再做 Sharding 会更好。

- [How to Scale Big Data Applications][52]
  - 这也是 Percona 给出的一篇关于怎样给大数据应用做架构扩展的文章。

- [MySQL Sharding with ProxySQL][53]
  - 用 ProxySQL 来支撑 MySQL 数据分片的一篇实践文章。

##### 缓存

- [缓存更新的套路][54]
  - 这是我在 CoolShell 上写的缓存更新的几个设计模式，包括 Cache Aside、Read/Write Through、Write Behind Caching。

- [Design Of A Modern Cache][55]
  - 设计一个现代化的缓存系统需要注意到的东西。

- [Netflix: Caching for a Global Netflix][56]
  - Netflix 公司的全局缓存架构实践。

- [Facebook: An analysis of Facebook photo caching][57]
  - Facebook 公司的图片缓存使用分析，这篇文章挺有意思的，用数据来调优不同的缓存大小和算法。

- [How trivago Reduced Memcached Memory Usage by 50%][58]
  - Trivago 公司一篇分享自己是如何把 Memcached 的内存使用率降了一半的实践性文章。

- [Caching Internal Service Calls at Yelp][59]
  - Yelp 公司的缓存系统架构。

##### 消息队列

- [Understanding When to use RabbitMQ or Apache Kafka][60]
  - 什么时候使用 RabbitMQ，什么时候使用 Kafka，通过这篇文章可以让你明白如何做技术决策。

- [Trello: Why We Chose Kafka For The Trello Socket Architecture][61]
  - Trello 的 Kafka 架构分享。

- [LinkedIn: Running Kafka At Scale][62]
  - LinkedIn 公司的 Kafka 架构扩展实践。

- [Should You Put Several Event Types in the Same Kafka Topic?][63]
  - 这个问题可能经常困扰你，这篇文章可以为你找到答案。

- [Billions of Messages a Day - Yelp’s Real-time Data Pipeline][64]
  - Yelp 公司每天十亿级实时消息的架构。

- [Uber: Building Reliable Reprocessing and Dead Letter Queues with Kafka][65]
  - Uber 公司的 Kafka 应用。

- [Uber: Introducing Chaperone: How Uber Engineering Audits Kafka End-to-End][66]
  - Uber 公司对 Kafka 消息的端到端审计。

- [Publishing with Apache Kafka at The New York Times][67]
  - 纽约时报的 Kafka 工程实践。

- [Kafka Streams on Heroku][68]
  - Heroku 公司的 Kafka Streams 实践。

- [Salesforce: How Apache Kafka Inspired Our Platform Events Architecture][69]
  - Salesforce 的 Kafka 工程实践。

- [Exactly-once Semantics are Possible: Here’s How Kafka Does it][70]
  - 怎样用 Kafka 让只发送一次的语义变为可能。这是业界中一个很难的工程问题。

- [Delivering billions of messages exactly once][71]
  - 这也是一篇挑战消息只发送一次这个技术难题的文章。

- [Benchmarking Streaming Computation Engines at Yahoo!][72]
  - Yahoo! 的 Storm 团队在为他们的流式计算做技术选型时，发现市面上缺乏针对不同计算平台的性能基准测试。
  - 于是，他们研究并设计了一种方案来做基准测试，测试了 Apache Flink、Apache Storm 和 Apache Spark 这三种平台。文中给出了结论和具体的测试方案。

##### 日志

- [Using Logs to Build a Solid Data Infrastructure - Martin Kleppmann][73]
  - 设计基于 log 结构应用架构的一篇不错的文章。

- [Building DistributedLog: High-performance replicated log service][74]
  - 这篇文章讲述了这个高性能日志系统的一些技术细节。
  - Distributed 是 Twitter 2016 年 5 月份开源的一个分布式日志系统。在 Twitter 内部已经使用 2 年多。
  - Distributed 主页：[distributedlog.io][75]
  - 其技术负责人是个中国人，他在微信公众号中也分享过这个系统 [Twitter 高性能分布式日志系统架构解析][76]。

- [LogDevice: a distributed data store for logs][77]
  - Facebook 分布式日志系统方面的一些工程分享。

##### 性能

- [Understand Latency][78]
  - 这篇文章收集并整理了一些和系统响应时间相关的文章，可以让你全面了解和 Latency 有关的系统架构和设计经验方面的知识。

- [Common Bottlenecks][79]
  - 文中讲述了 20 个常见的系统瓶颈。

- [Performance is a Feature][80]
  - Coding Horror 上的一篇让你关注性能的文章。

- [Make Performance Part of Your Workflow][81]
  - 这篇文章是图书[《Designing for Performance》][115]中的节选（国内没有卖的），其中给出来了一些和性能有关的设计上的平衡和美学。

- [CloudFlare: How we built rate limiting capable of scaling to millions of domain][82]
  - 讲述了 CloudFlare 公司是怎样实现他们的限流功能的。

##### 搜索

- [Instagram: Search Architecture][83]
- [eBay: The Architecture of eBay Search][84]
- [eBay: Improving Search Engine Efficiency by over 25%][85]
- [LinkedIn: Introducing LinkedIn’s new search architecture][86]
- [LinkedIn: Search Federation Architecture at LinkedIn][87]
- [Slack: Search at Slack][88]
- [DoorDash: Search and Recommendations at DoorDash][89]
- [Twitter: Search Service at Twitter (2014)][90]
- [Pinterest: Manas: High Performing Customized Search System][91]
- [Sherlock: Near Real Time Search Indexing at Flipkart][92]
- [Airbnb: Nebula: Storage Platform to Build Search Backends][93]

##### 各公司的架构实践

- [High Scalability][94]
  - 这个网站会定期分享一些大规模系统架构是怎样构建的，下面是迄今为止各个公司的架构说明。

- [YouTube Architecture][95]
- [Scaling Pinterest][96]
- [Google Architecture][97]
- [Scaling Twitter][98]
- [The WhatsApp Architecture][99]
- [Flickr Architecture][100]
- [Amazon Architecture][101]
- [Stack Overflow Architecture][102]
- [Pinterest Architecture][103]
- [Tumblr Architecture][104]
- [Instagram Architecture][105]
- [TripAdvisor Architecture][106]
- [Scaling Mailbox][107]
- [Salesforce Architecture ESPN Architecture][108]
- [Uber Architecture][109]
- [Dropbox Design][110]
- [Splunk Architecture][111]

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

  [1]: https://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf
  [2]: https://www.youtube.com/watch?v=modXC5IWTJI
  [3]: https://12factor.net/
  [4]: https://12factor.net/zh_cn/
  [5]: https://www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/
  [6]: https://www.usenix.org/legacy/event/lisa07/tech/full_papers/hamilton/hamilton_html/index.html
  [7]: https://cloud.tencent.com/developer/article/1685096
  [8]: https://blog.box.com/4-things-keep-mind-when-building-platform-enterprise
  [9]: https://www.usenix.org/conference/srecon17americas/program/presentation/rosenthal
  [10]: https://www.igvita.com/2016/05/20/building-fast-and-resilient-web-applications/
  [12]: http://highscalability.com/blog/2012/12/31/designing-for-resiliency-will-be-so-2013.html
  [13]: https://learn.microsoft.com/en-us/azure/architecture/guide/design-principles/
  [14]: https://www.allthingsdistributed.com/2008/12/eventually_consistent.html
  [15]: https://www.codeproject.com/Articles/151520/Write-Scalable-Code
  [16]: https://architecht.io/lessons-from-facebook-on-engineering-for-scale-f5716f0afc7a
  [17]: https://learn.microsoft.com/en-us/azure/architecture/patterns/
  [18]: https://learn.microsoft.com/en-us/azure/architecture/framework/resiliency/reliability-patterns
  [19]: https://learn.microsoft.com/en-us/azure/architecture/patterns/category/data-management
  [20]: https://learn.microsoft.com/en-us/azure/architecture/patterns/category/design-implementation
  [21]: https://learn.microsoft.com/en-us/azure/architecture/patterns/category/messaging
  [22]: https://learn.microsoft.com/en-us/azure/architecture/patterns/category/management-monitoring
  [23]: https://learn.microsoft.com/en-us/azure/architecture/framework/scalability/
  [24]: https://learn.microsoft.com/en-us/azure/architecture/framework/resiliency/reliability-patterns
  [25]: https://learn.microsoft.com/en-us/azure/architecture/framework/security/
  [26]: https://en.clouddesignpattern.org/index.php/Main_Page
  [27]: https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/45406.pdf
  [28]: https://www.slideshare.net/pagsousa/patterns-fro-distributed-systems
  [29]: https://microservices.io/patterns/index.html
  [30]: https://patterns.arcitura.com/soa-patterns
  [31]: https://medium.com/netflix-techblog/fit-failure-injection-testing-35d8e2a9bb2
  [32]: https://netflixtechblog.com/automated-failure-testing-86c1b8bc841f
  [33]: https://people.ucsc.edu/~palvaro/socc16.pdf
  [34]: http://highscalability.com/blog/2014/5/12/4-architecture-issues-when-scaling-web-applications-bottlene.html
  [35]: http://ithare.com/scaling-stateful-objects/
  [36]: https://blog.codinghorror.com/scaling-up-vs-scaling-out-hidden-costs/
  [37]: https://www.infoq.cn/article/hiXg6WRDjvNE0VNuwzPg
  [38]: https://www.infoq.com/articles/scalability-worst-practices/
  [39]: http://highscalability.com/blog/2013/8/26/reddit-lessons-learned-from-mistakes-made-scaling-to-1-billi.html
  [40]: https://medium.com/pinterest-engineering/auto-scaling-pinterest-df1d2beb4d64
  [41]: https://medium.com/square-corner-blog/autoscaling-based-on-request-queuing-c4c0f57f860f
  [42]: https://medium.com/paypal-tech/autoscaling-applications-paypal-fb5bb9fdb821
  [43]: https://tech.trivago.com/post/autoscaling-jenkins-guide/
  [44]: https://netflixtechblog.com/scryer-netflixs-predictive-auto-scaling-engine-a3f8fc922270
  [45]: http://tom-e-white.com/2007/11/consistent-hashing.html
  [46]: https://dgryski.medium.com/consistent-hashing-algorithmic-tradeoffs-ef6b8e2fcae8
  [47]: https://netflixtechblog.com/distributing-content-to-open-connect-3e3e391d4dc9
  [48]: https://blog.imaginea.com/consistent-hashing-in-cassandra/
  [49]: https://queue.acm.org/detail.cfm?id=3025012
  [50]: https://medium.com/@jeeyoungk/how-sharding-works-b4dec46b3f6
  [51]: https://www.percona.com/blog/2009/08/06/why-you-dont-want-to-shard/
  [52]: https://www.percona.com/sites/default/files/presentations/How%20to%20Scale%20Big%20Data%20Applications.pdf
  [53]: https://www.percona.com/blog/2016/08/30/mysql-sharding-with-proxysql/
  [54]: https://coolshell.cn/articles/17416.html
  [55]: http://highscalability.com/blog/2016/1/25/design-of-a-modern-cache.html
  [56]: https://netflixtechblog.com/caching-for-a-global-netflix-7bcc457012f1
  [57]: https://engineering.fb.com/2014/02/20/web/an-analysis-of-facebook-photo-caching/
  [58]: https://tech.trivago.com/post/2017-12-19-memcached-optimization/
  [59]: https://engineeringblog.yelp.com/2018/03/caching-internal-service-calls-at-yelp.html
  [60]: https://tanzu.vmware.com/developer/blog/understanding-the-differences-between-rabbitmq-vs-kafka/
  [61]: https://tech.trello.com/why-we-chose-kafka/
  [62]: https://engineering.linkedin.com/kafka/running-kafka-scale
  [63]: https://www.confluent.io/blog/put-several-event-types-kafka-topic/
  [64]: https://engineeringblog.yelp.com/2016/07/billions-of-messages-a-day-yelps-real-time-data-pipeline.html
  [65]: https://www.uber.com/en-JP/blog/reliable-reprocessing/
  [66]: https://www.uber.com/en-JP/blog/chaperone-audit-kafka-messages/
  [67]: https://open.nytimes.com/publishing-with-apache-kafka-at-the-new-york-times-7f0e3b7d2077
  [68]: https://blog.heroku.com/kafka-streams-on-heroku
  [69]: https://engineering.salesforce.com/how-apache-kafka-inspired-our-platform-events-architecture-2f351fe4cf63/
  [70]: https://www.confluent.io/blog/exactly-once-semantics-are-possible-heres-how-apache-kafka-does-it/
  [71]: https://segment.com/blog/exactly-once-delivery/
  [72]: https://yahooeng.tumblr.com/post/135321837876/benchmarking-streaming-computation-engines-at
  [73]: https://www.confluent.io/blog/using-logs-to-build-a-solid-data-infrastructure-or-why-dual-writes-are-a-bad-idea/
  [74]: https://blog.twitter.com/engineering/en_us/topics/infrastructure/2015/building-distributedlog-twitter-s-high-performance-replicated-log-servic
  [75]: https://github.com/twitter-archive/distributedlog
  [76]: https://mp.weixin.qq.com/s?__biz=MzAwMDU1MTE1OQ==&mid=403051208&idx=1&sn=1694ac05acbcb5ca53c88bfac8a68856&scene=2&srcid=1224xZuQ9QQ4sRmiPVdHTppL
  [77]: https://engineering.fb.com/2017/08/31/core-data/logdevice-a-distributed-data-store-for-logs/
  [78]: http://highscalability.com/latency-everywhere-and-it-costs-you-sales-how-crush-it
  [79]: http://highscalability.com/blog/2012/5/16/big-list-of-20-common-bottlenecks.html
  [80]: https://blog.codinghorror.com/performance-is-a-feature/
  [81]: https://www.etsy.com/codeascraft/make-performance-part-of-your-workflow/
  [82]: https://blog.cloudflare.com/counting-things-a-lot-of-different-things/
  [83]: https://instagram-engineering.com/search-architecture-eeb34a936d3a
  [84]: http://www.cs.otago.ac.nz/homepages/andrew/papers/2017-8.pdf
  [85]: https://tech.ebayinc.com/research/making-e-commerce-search-faster/
  [86]: https://engineering.linkedin.com/search/did-you-mean-galene
  [87]: https://engineering.linkedin.com/blog/2018/03/search-federation-architecture-at-linkedin
  [88]: https://slack.engineering/search-at-slack/
  [89]: https://doordash.news/company/powering-search-recommendations-at-doordash/
  [90]: https://blog.twitter.com/engineering/en_us/a/2014/building-a-complete-tweet-index
  [91]: https://medium.com/pinterest-engineering/manas-a-high-performing-customized-search-system-cf189f6ca40f
  [92]: https://blog.flipkart.tech/
  [93]: https://medium.com/airbnb-engineering/nebula-as-a-storage-platform-to-build-airbnbs-search-backends-ecc577b05f06
  [94]: http://highscalability.com/
  [95]: http://highscalability.com/youtube-architecture
  [96]: http://highscalability.com/blog/2013/4/15/scaling-pinterest-from-0-to-10s-of-billions-of-page-views-a.html
  [97]: http://highscalability.com/google-architecture
  [98]: http://highscalability.com/scaling-twitter-making-twitter-10000-percent-faster
  [99]: http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html
  [100]: http://highscalability.com/flickr-architecture
  [101]: http://highscalability.com/amazon-architecture
  [102]: http://highscalability.com/blog/2009/8/5/stack-overflow-architecture.html
  [103]: http://highscalability.com/blog/2012/5/21/pinterest-architecture-update-18-million-visitors-10x-growth.html
  [104]: http://highscalability.com/blog/2012/2/13/tumblr-architecture-15-billion-page-views-a-month-and-harder.html
  [105]: http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html
  [106]: http://highscalability.com/blog/2011/6/27/tripadvisor-architecture-40m-visitors-200m-dynamic-page-view.html
  [107]: http://highscalability.com/blog/2013/6/18/scaling-mailbox-from-0-to-one-million-users-in-6-weeks-and-1.html
  [108]: http://highscalability.com/blog/2013/9/23/salesforce-architecture-how-they-handle-13-billion-transacti.html
  [109]: http://highscalability.com/blog/2015/9/14/how-uber-scales-their-real-time-market-platform.html
  [110]: https://www.youtube.com/watch?v=PE4gwstWhmc
  [111]: https://www.splunk.com/en_us/products/splunk-enterprise.html?301=/view/SP-CAAABF9
  [112]: https://learn.microsoft.com/en-us/azure/architecture/guide/design-principles/self-healing
  [113]: https://learn.microsoft.com/en-us/azure/architecture/guide/design-principles/scale-out
  [114]: https://learn.microsoft.com/en-us/azure/architecture/guide/design-principles/design-for-evolution
  [115]: https://www.oreilly.com/library/view/designing-for-performance/9781491903704/

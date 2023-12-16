# 《程序员练级攻略》分析笔记

## 第12章 分布式架构入门

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- 分布式系统涵盖的知识点
- 分布式系统的注意事项
- 分布式架构入门
- 分布式理论

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 分布式系统涵盖的知识点

- **服务调度**，涉及服务发现、配置管理、弹性伸缩、故障恢复等。
- **资源调度**，涉及对底层资源的调度使用，如计算资源、网络资源和存储资源等。
- **流量调度**，涉及路由、负载均衡、流控、熔断等。
- **数据调度**，涉及数据复本、数据一致性、分布式事务、分库、分表等。
- **容错处理**，涉及隔离、幂等、重试、业务补偿、异步、降级等。
- **自动化运维**，涉及持续集成、持续部署、全栈监控、调用链跟踪等。

#### 分布式系统的注意事项

- 分布式系统之所以复杂，就是因为它太容易出错了。这意味着，你要把处理错误的代码当成正常功能的代码来处理。
- 开发一个健壮的分布式系统的成本是单体系统的几百倍甚至几万倍。这意味着，我们要自己开发一个，需要能力很强的开发人员。
- 非常健壮的开源的分布式系统并不多，或者说基本没有。这意味着，如果你要用开源的，那么你需要 hold 得住其源码。
- 管理或是协调多个服务或机器是非常难的。这意味着，我们要去读很多很多的分布式系统的论文。
- 在分布式环境下，出了问题是很难 debug 的。这意味着，我们需要非常好的监控和跟踪系统，还需要经常做演练和测试。
- 在分布式环境下，你需要更科学地分析和统计。这意味着，我们要用 P90 这样的统计指标，而不是平均值，我们还需要做容量计划和评估。
- 在分布式环境下，需要应用服务化。这意味着，我们需要一个服务开发框架，比如 SOA 或微服务。
- 在分布式环境下，故障不可怕，可怕的是影响面过大，时间过长。这意味着，我们需要花时间来开发我们的自动化运维平台。

- 耐性和坚强
  - 在分布式环境下，一切都变得非常复杂。
  - 要进入这个领域，你需要有足够多的耐性和足够强的心态来接受各式各样的失败。
  - 当拥有丰富的实践和经验后，你才会有所建树。
  - 这并不是一日之功，你可能要在这个领域花费数年甚至数十年的时间。

#### 分布式架构入门

- 架构设计的基本概念
  - [Scalable Web Architecture and Distributed Systems][1]: 这篇文章会给你一个大概的分布式架构是怎么来解决系统扩展性问题的粗略方法。
  - [Scalability, Availability & Stability Patterns][2]: 这个 PPT 能在扩展性、可用性、稳定性等方面给你一个非常大的架构设计视野和思想，可以让你感受一下大概的全景图。

- [System Design Primer][3]
  - 这个仓库主要收集分布式系统的一些与扩展性相关的资源，它可以帮助你学习如何构建可扩展的架构。
  - 目前这个仓库收集到了好些系统架构和设计的基本方法。其中包括：
    CAP 理论、一致性模型、可用性模式、DNS、CDN、负载均衡、反向代理、应用层的微服务和服务发现、关系型数据库和 NoSQL、缓存、异步通讯、安全等。

#### 分布式理论

- [An introduction to distributed systems][4]
  - 这只是某个教学课程的提纲，但几乎涵盖了分布式系统方面的所有知识点，而且辅以简洁并切中要害的说明文字，非常适合初学者提纲挈领地了解知识全貌，快速与现有知识结合，形成知识体系。
  - 这也是一个分布式系统的知识图谱，可以让你看到分布式系统的整体全貌。你可以根据这个知识图 Google 下去，然后你会学会所有的东西。

- [Byzantine Generals Problem][5]
  - 这个问题是莱斯利·兰波特（Leslie Lamport）于 1982 年提出用来解释一致性问题的一个虚构模型（[论文地址][25]）。
  - [Dr.Dobb’s - The Byzantine Generals Problem][6]
  - [The Byzantine Generals Problem][7] （翻墙打不开）
  - [Practicle Byzantine Fault Tolerance][8]

- 拜占庭容错系统研究中有三个重要理论：CAP、FLP 和 DLS。
  - [CAP 定理][9]: 分布式数据存储不可能同时满足以下三个条件：一致性（Consistency）、可用性（Availability）和 分区容忍（Partition tolerance）。
  - [FLP impossibility][12]: 在异步环境中，如果节点间的网络延迟没有上限，只要有一个恶意的节点存在，就没有算法能在有限的时间内达成共识。
    - ["Las Vegas" algorithms][13]
      （这个算法又叫撞大运算法，其保证结果正确，只是在运算时所用资源上进行赌博，一个简单的例子是随机快速排序，它的 pivot 是随机选的，但排序结果永远一致）
      在每一轮皆有一定机率达成共识，随着时间增加，机率会越趋近于 1。而这也是许多成功的共识算法会采用的解决问题的办法。
  - [DLS 论文][14]: 讨论容错的上限
    - [randomized algorithms][15]: 在这种情况下可以容忍最多 1/3 的拜占庭故障。

- [8 条荒谬的分布式假设（Fallacies of Distributed Computing）][16]
  - 网络是稳定的。
  - 网络传输的延迟是零。
  - 网络的带宽是无穷大。
  - 网络是安全的。
  - 网络的拓扑不会改变。
  - 只有一个系统管理员。
  - 传输数据的成本为零。
  - 整个网络是同构的。

- 对 8 条荒谬的分布式假设的解释
  - [Fallacies of Distributed Computing Explained][17]：解释为什么这些观点是错误的。
  - [加勒思·威尔逊（Gareth Wilson）的文章][18]： 用日常生活中的例子对这些点做了通俗的解释。

- 几篇一致性方面的论文
  - [CAP Twelve Years Later: How the Rules Have Changed][19] （[中译版][20]）
    - 在 CAP 中最大的问题就是分区（也就是 P），在 P 发生的情况下，非常难以保证 C 和 A。然而，这是强一致性的情况。
  - [Harvest, Yield, and Scalable Tolerant Systems][21]
    - 主要提出了 Harvest 和 Yield 概念。
  - [Base: An Acid Alternative][22]（[中译版][23]）
    - 解释 BASE 原则，或者说最终一致性。
  - [Eventually Consistent][24]
    - 阐述了 NoSQL 数据库的理论基石——最终一致性，对传统的关系型数据库（ACID，Transaction）做了较好的补充。

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

  [1]: http://www.aosabook.org/en/distsys.html
  [2]: http://www.slideshare.net/jboner/scalability-availability-stability-patterns
  [3]: https://github.com/donnemartin/system-design-primer
  [4]: https://github.com/aphyr/distsys-class
  [5]: https://en.wikipedia.org/wiki/Byzantine_fault
  [6]: https://www.drdobbs.com/cpp/the-byzantine-generals-problem/206904396
  [7]: http://blog.jameslarisch.com/the-byzantine-generals-problem
  [8]: https://pmg.csail.mit.edu/papers/osdi99.pdf
  [9]: https://en.wikipedia.org/wiki/CAP_theorem
  [12]: https://www.the-paper-trail.org/post/2008-08-13-a-brief-tour-of-flp-impossibility/
  [13]: https://en.wikipedia.org/wiki/Las_Vegas_algorithm
  [14]: http://groups.csail.mit.edu/tds/papers/Lynch/jacm88.pdf
  [15]: https://link.springer.com/chapter/10.1007/978-3-540-77444-0_7
  [16]: https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing
  [17]: https://arnon.me/wp-content/uploads/Files/fallacies.pdf
  [18]: https://shimo.im/docs/gYpKDyQv6CXGgHTr/read
  [19]: https://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed/
  [20]: https://www.infoq.cn/article/cap-twelve-years-later-how-the-rules-have-changed/
  [21]: https://www.semanticscholar.org/paper/Harvest%2C-yield%2C-and-scalable-tolerant-systems-Fox-Brewer/9c9ceb29a358149e9617d103f5624f325bf08b1e?p2df
  [22]: https://queue.acm.org/detail.cfm?id=1394128
  [23]: https://www.cnblogs.com/savorboard/p/base-an-acid-alternative.html
  [24]: https://www.allthingsdistributed.com/2008/12/eventually_consistent.html
  [25]: https://www.microsoft.com/en-us/research/uploads/prod/2016/12/The-Byzantine-Generals-Problem.pdf

# 《程序员练级攻略》分析笔记

## 第7章 软件设计

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

介绍软件设计的一些知识和资料。

### Q3：这一章的大纲是什么

- 编程范式
- 一些软件设计的相关原则
- 一些软件设计的读物

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

- 要学好这些软件开发和设计的方法，
  你真的需要磨练和苦行，反复咀嚼，反复推敲，在实践和理论中螺旋式地学习，才能真正掌握。

#### 编程范式

- [陈皓「极客时间」课程：《编程范式游记》][1]

- [Wikipedia: Programming paradigm][2]

- [Six programming paradigms that will change how you think about coding][3]
  - 中文翻译版为 [六个编程范型将改变你对编程的看法][4]

- [Programming Paradigms for Dummies: What Every Programmer Should Know][5]

- [斯坦福大学公开课：编程范式][6]

#### 一些软件设计的相关原则

- [Don’t Repeat Yourself (DRY)][7]

- [Keep It Simple, Stupid(KISS)][8]

- [Program to an interface, not an implementation][9]
  - 这是设计模式中最根本的哲学，注重接口，而不是实现，依赖接口，而不是实现。

- [You Ain’t Gonna Need It (YAGNI)][10]
  - 只考虑和设计必须的功能，避免过度设计。

- [Law of Demeter][11]
  - 又称“最少知识原则”
  - 克雷格·拉尔曼（Craig Larman）把 Law of Demeter 又称作“不要和陌生人说话”。
  - 关于迪米特法则有一些很形象的比喻：
    - 如果你想让你的狗跑的话，你会对狗狗说还是对四条狗腿说？
    - 如果你去店里买东西，你会把钱交给店员，还是会把钱包交给店员让他自己拿？

- [面向对象的 S.O.L.I.D 原则][12]
  - SRP（Single Responsibility Principle）- 职责单一原则
  - OCP（Open/Closed Principle）- 开闭原则。模块是可扩展的，而不可修改的。也就是说，对扩展是开放的，而对修改是封闭的。
  - LSP（Liskov substitution principle）- 里氏代换原则。Robert C. Martin 将其简化为一句话：“Subtypes must be substitutable for their base types”。
  - ISP（Interface Segregation Principle ）- 接口隔离原则。把功能实现在接口中，而不是类中，使用多个专门的接口比使用单一的总接口要好。
  - DIP（Dependency Inversion Principle）- 依赖倒置原则。高层模块不应该依赖于低层模块的实现，而是依赖于高层抽象。

- [CCP（Common Closure Principle） - 共同封闭原则][13]
  - 一个包中所有的类应该对同一种类型的变化关闭。一个变化影响一个包，便影响了包中所有的类。
  - 一个更简短的说法是：一起修改的类，应该组合在一起（同一个包里）。

- [CRP（Common Reuse Principle）- 共同重用原则][14]
  - 包的所有类被一起重用。如果你重用了其中的一个类，就重用全部。
  - 换个说法是，没有被一起重用的类不应该组合在一起。

- [Hollywood Principle - 好莱坞原则][15]
  - “Don’t call us, we’ll call you.”。
  - 所有的组件都是被动的，所有的组件初始化和调用都由容器负责。
  - 好莱坞原则就是 [IoC（Inversion of Control）][16] 或 [DI（Dependency Injection）][17] 的基础原则。

- [High Cohesion & Low/Loose coupling - 高内聚， 低耦合][18]
  - [马萨诸塞州戈登学院的面向对象课中的其中一节讲义：High Cohesion and Low Coupling][19]

- [CoC（Convention over Configuration）- 惯例优于配置原则][40]
  - 将一些公认的配置方式和信息作为内部缺省的规则来使用。
  - 例如，Hibernate 的映射文件，如果约定字段名和类属性一致的话，基本上就可以不要这个配置文件了。

- [SoC (Separation of Concerns) - 关注点分离][20]

- [DbC（Design by Contract）- 契约式设计][21]

- [ADP（Acyclic Dependencies Principle）- 无环依赖原则][22]

#### 一些软件设计的读物

- [《领域驱动设计》][23]

- [《UNIX 编程艺术》][24]

- [The Clean Architecture (Blog)][25]
  - [The Clean Architecture (Book)][26]

- [The Twelve-Factor App][27]
  - [The Twelve-Factor App（中文版）][28]

- [Avoid Over Engineering][29]

- [Instagram Engineering’s 3 rules to a scalable cloud application architecture][30]
  - Instagram 工程的三个黄金法则：1）使用稳定可靠的技术（迎接新的技术）；2）不要重新发明轮子；3）Keep it very simple。
  - Amazon 也有两条工程法则，一个是自动化，一个是简化。

- [How To Design A Good API and Why it Matters - Joshua Bloch][31]

- Restful API
  - [Best Practices for Designing a Pragmatic RESTful API][32]
  - [Ideal REST API design][33]
  - [HTTP API Design Guide][34]
  - [Microsoft REST API Guidelines][35]
  - [IBM Watson REST API Guidelines][36]
  - [Zalando RESTful API and Event Scheme Guidelines][37]

- [The Problem With Logging][38]: 一篇关于程序打日志的短文，可以让你知道一些可能以往不知道的打日志需要注意的问题。

- [Concurrent Programming for Scalable Web Architectures][39]: 这是一本在线的免费书，教你如何架构一个可扩展的高性能的网站。其中谈到了一些不错的设计方法和知识。

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

  [1]: https://time.geekbang.org/column/article/301
  [2]: https://en.wikipedia.org/wiki/Programming_paradigm
  [3]: https://www.ybrikman.com/writing/2014/04/09/six-programming-paradigms-that-will/
  [4]: https://blog.51cto.com/u_15127629/2899729
  [5]: https://www.info.ucl.ac.be/~pvr/VanRoyChapter.pdf
  [6]: https://open.163.com/newview/movie/free?pid=SFTLSEVA0&mid=SFTLVUD90
  [7]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
  [8]: https://en.wikipedia.org/wiki/KISS_principle
  [9]: https://stackoverflow.com/questions/2697783/what-does-program-to-interfaces-not-implementations-mean
  [10]: https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it
  [11]: https://en.wikipedia.org/wiki/Law_of_Demeter
  [12]: https://en.wikipedia.org/wiki/SOLID
  [13]: http://wiki.c2.com/?CommonClosurePrinciple
  [14]: http://wiki.c2.com/?CommonReusePrinciple
  [15]: https://en.wiktionary.org/wiki/Hollywood_principle
  [16]: https://en.wikipedia.org/wiki/Inversion_of_control
  [17]: https://martinfowler.com/articles/injection.html
  [18]: https://en.wikipedia.org/wiki/Coupling_(computer_programming)
  [19]: https://www.math-cs.gordon.edu/courses/cs211/lectures-2009/Cohesion,Coupling,MVC.pdf
  [20]: http://sulong.me/archives/99
  [21]: https://en.wikipedia.org/wiki/Design_by_contract
  [22]: http://wiki.c2.com/?AcyclicDependenciesPrinciple
  [23]: https://book.douban.com/subject/26819666/
  [24]: https://book.douban.com/subject/1467587/
  [25]: https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
  [26]: https://book.douban.com/subject/26915970/
  [27]: https://12factor.net/
  [28]: https://12factor.net/zh_cn/
  [29]: https://medium.com/@rdsubhas/10-modern-software-engineering-mistakes-bc67fbef4fc8
  [30]: https://datastax.medium.com/instagram-engineerings-3-rules-to-a-scalable-cloud-application-architecture-c44afed31406
  [31]: https://www.infoq.com/presentations/effective-api-design/
  [32]: https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
  [33]: https://betimdrenica.wordpress.com/2015/03/09/ideal-rest-api-design/
  [34]: https://github.com/interagent/http-api-design
  [35]: https://github.com/Microsoft/api-guidelines/blob/vNext/Guidelines.md
  [36]: https://github.com/watson-developer-cloud/api-guidelines
  [37]: https://opensource.zalando.com/restful-api-guidelines/
  [38]: https://blog.codinghorror.com/the-problem-with-logging/
  [39]: http://berb.github.io/diploma-thesis/community/index.html
  [40]: https://en.wikipedia.org/wiki/Convention_over_configuration

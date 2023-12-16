# 《程序员练级攻略》分析笔记

## 第4章 编程语言

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

介绍几门常用的编程语言的学习方法及资料。

### Q3：这一章的大纲是什么

- Java
- C
- C++
- Go

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### Java

- [《Java 核心技术：卷 1 基础知识》][1]: 这本书本来是 Sun 公司的官方用书，是一本 Java 的入门参考书。
  - 对于 Java 初学者来说，是一本非常不错的值得时常翻阅的技术手册。书中有较多地方进行 Java 与 C++ 的比较。

- [《Spring 实战》][2] 和 [《Spring Boot 实战》][3]：前者是传统的 Spring，后者是新式的微服务的 Spring。如果你只想看一本的话，那么就看后者吧。

- [《Effective Java》][4]: 学习编写高效的代码。

- [Google Guava 库 ][5]
  - 这个库不但是 JDK 的升级库，其中有如：
    集合（collections）、缓存（caching）、原生类型支持（primitives support）、并发库（concurrency libraries）、通用注解（common annotations）、字符串处理（string processing）、I/O 等库，
  - 还是 Effective Java 这本书中的那些经验的实践代表。

- [《Java 并发编程实战》][6]: 是一本完美的 Java 并发参考手册。
  - 书中从并发性和线程安全性的基本概念出发，介绍了如何使用类库提供的基本并发构建块，用于避免并发危险、构造线程安全的类及验证线程安全的规则，
  - 如何将小的线程安全类组合成更大的线程安全类，
  - 如何利用线程来提高并发应用程序的吞吐量，
  - 如何识别可并行执行的任务，
  - 如何提高单线程子系统的响应性，
  - 如何确保并发程序执行预期任务，
  - 如何提高并发代码的性能和可伸缩性等。
  - 最后介绍了一些高级主题，如显式锁、原子变量、非阻塞算法以及如何开发自定义的同步工具类。

- [《Java 性能权威指南》][7]: 通过学习这本书，你可以比较大程度地提升性能测试的效果。

- [《深入理解 Java 虚拟机》][8]: 了解更多的底层细节。

- [《Java 编程思想》][9]: 从宏观角度了解 Java。

- [《精通 Spring 4.x》][10]:
  - 一本很不错的书，就是有点厚，一共有 800 多页，都是干货。
  - 我认为其中最不错的是在分析原理，尤其是针对前面提到的 Spring 技术，应用与原理都讲得很透彻，IOC 和 AOP 也分析得很棒，娓娓道来。

- 学 Java 你一定要学面向对象的设计模式。
  - [《设计模式》][11]
  - [《Head First 设计模式》][12]

- Program to an 'interface', not an 'implementation'.
  - 使用者不需要知道数据类型、结构、算法的细节。
  - 使用者不需要知道实现细节，只需要知道提供的接口。
  - 利于抽象、封装，动态绑定，多态。符合面向对象的特质和理念。

- Favor 'object composition' over 'class inheritance'.
  - 继承需要给子类暴露一些父类的设计和实现细节。
  - 父类实现的改变会造成子类也需要改变。
  - 我们以为继承主要是为了代码重用，但实际上在子类中需要重新实现很多父类的方法。
  - 继承更多的应该是为了多态。

#### C

- [《C 程序设计语言》][13]

- [《C 语言程序设计现代方法》][14]

- [《C 陷阱与缺陷》][15]

#### C++

- [《C++ 的坑真的多吗？》][16]

- [《C++ Primer 中文版》][17]

- [《Effective C++》][18]

- [《More Effective C++》][19]

- [《深度探索 C++ 对象模型》][20]
  - [《C++ 虚函数表解析》][21]
  - [《C++ 对象内存布局》][22]

- [《C++ FAQ》][23]
  - [《C++ FAQ》（中文版）][24]

#### Go

- [《Go by Example》][25]

- [《Go 101》][26]

- [《The Go Programming Language》][27]

- 酷壳的两篇 Go 入门博客
  - [GO 语言简介（上）- 语法][28]
  - [GO 语言简介（下）- 特性][29]

- [《Effective Go》][30]

- Rob Pike 在 Google I/O 的两个分享
  - Go Concurrency Patterns（[幻灯片][31] 和 [演讲视频][32]）。
  - Advanced Go Concurrency Patterns（[幻灯片][33]、[演讲视频][34]）。

- Go wiki
  - [Go 精华文章列表][35]
  - [Go 相关博客列表][36]
  - [Go Talks][37]

- [Awesome Go][38]

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

  [1]: https://book.douban.com/subject/26880667/
  [2]: https://book.douban.com/subject/26767354/
  [3]: https://book.douban.com/subject/26857423/
  [4]: https://book.douban.com/subject/27047716/
  [5]: https://github.com/google/guava
  [6]: https://book.douban.com/subject/10484692/
  [7]: https://book.douban.com/subject/26740520/
  [8]: https://book.douban.com/subject/24722612/
  [9]: https://book.douban.com/subject/2130190/
  [10]: https://book.douban.com/subject/26952826/
  [11]: https://book.douban.com/subject/1052241/
  [12]: https://book.douban.com/subject/2243615/
  [13]: https://book.douban.com/subject/1139336/
  [14]: https://book.douban.com/subject/2280547/
  [15]: https://en.wikipedia.org/wiki/The_C_Programming_Language
  [16]: https://book.douban.com/subject/2778632/
  [17]: https://coolshell.cn/articles/7992.html
  [18]: https://book.douban.com/subject/25708312/
  [19]: https://book.douban.com/subject/5908727/
  [20]: https://book.douban.com/subject/10427315/
  [21]: https://coolshell.cn/articles/12165.html
  [22]: https://coolshell.cn/articles/12176.html
  [23]: https://www.stroustrup.com/bs_faq.html
  [24]: https://www.stroustrup.com/bsfaqcn.html
  [25]: https://gobyexample.com/
  [26]: https://go101.org/article/101.html
  [27]: https://book.douban.com/subject/26337545/
  [28]: https://coolshell.cn/articles/8460.html
  [29]: https://coolshell.cn/articles/8489.html
  [30]: https://go.dev/doc/effective_go
  [31]: https://go.dev/talks/2012/concurrency.slide#1
  [32]: https://www.youtube.com/watch?v=f6kdp27TYZs
  [33]: https://go.dev/talks/2013/advconc.slide#1
  [34]: https://www.youtube.com/watch?v=QDDwwePbDtw
  [35]: https://github.com/golang/go/wiki/Articles
  [36]: https://github.com/golang/go/wiki/Blogs
  [37]: https://github.com/golang/go/wiki/GoTalks
  [38]: https://github.com/avelino/awesome-go

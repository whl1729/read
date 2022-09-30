# 《程序员练级攻略》分析笔记

## 第10章 Java 底层知识

### Q1：这一章的内容属于哪一类别？

计算机/方法论。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- Java 字节码
- JVM

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### Java 字节码

- Java 黑科技
  - Java 最黑科技的玩法就是字节码编程，也就是动态修改或是动态生成 Java 字节码。
  - Java 的字节码相当于汇编。

- Java 字节码教程
  - [Java Zone: Introduction to Java Bytecode][1]: 这篇文章图文并茂地向你讲述了 Java 字节码的一些细节，是一篇很不错的入门文章。
  - [IBM DeveloperWorks: Java bytecode][2]: 虽然这篇文章很老了，但是这篇文章是一篇非常好的讲 Java 字节码的文章。
  - [Java Bytecode and JVMTI Example][3]: 这是一些使用 [JVM Tool Interface][23] 操作字节码的比较实用的例子。包括方法调用统计、静态字节码修改、Heap Taggin 和 Heap Walking。

- Java 字节码相关库
  - [asmtools][4]: 用于生产环境的 Java .class 文件开发工具。
  - [Byte Buddy][5]: 代码生成库：运行时创建 Class 文件而不需要编译器帮助。（作者最喜欢）
  - [Jitescript][6]: 和 [BiteScript][24] 类似的字节码生成库。

- 字节码编程的高级玩法
  - 在 Java 程序运行时进行字节码修改和代码注入
  - 比如把我们的监控代码直接以字节码的方式注入到别人的代码中，从而实现对实际程序运行情况进行统计和监控
  - 以很魔法地把业务逻辑和代码控制分离开来

- Java Agent
  - Java Agent 使用的是 [Java Instrumentation API][7]，其主要方法是实现一个叫 premain() 的方法，然后把你的代码编译成一个 jar 文件。
  - [Java Code Geeks: Java Agents][8]
  - [jvm-monitoring-agent][9]：示例项目1
  - [EntryPointKR/Agent.java][10]：示例项目2
  - [通过使用 Byte Buddy，便捷地创建 Java Agent][11]
  - [Stage Monitor][12]：使用 Java Agent 做监控

#### JVM

- JVM 规格说明书（有必要阅读）
  - [The Java Virtual Machine Specification Java SE 8 Edition][13]
  - [java-virtual-machine-specification][14]：中文版

- [JVM Anatomy Park（JVM 解剖公园）][15]
  - 一个系列的文章，每篇文章都不长，但是都很精彩，带你一点一点地把 JVM 中的一些技术解开。

- Java 的内存模型
  - [JSR 133][16]：官方文章
  - [The Java Memory Model][17]：马里兰大学的威廉·皮尤（William Pugh）教授收集的和 Java 内存模型相关的文献 
  - [The JSR-133 Cookbook for Compiler Writer][18]: 解释了怎样实现 Java 内存模型，特别是在考虑到多处理器（或多核）系统的情况下，多线程和读写屏障的实现。
  - [Using JDK 9 Memory Order Mode][19]: 讲了怎样通过 VarHandle 来使用 plain、opaque、release/acquire 和 volatile 四种共享内存的访问模式，并剖析了底层的原理。

- 垃圾回收机制
  - [《The Garbage Collection Handbook》][20]

- 垃圾回收调优
  - [Garbage Collection Tuning Guide][21]: Hotspot Java 虚拟机的垃圾回收调优指南。

- [Quick Tips for Fast Code on the JVM][22]

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

  [1]: https://dzone.com/articles/introduction-to-java-bytecode
  [2]: https://developer.ibm.com/technologies/web-development/
  [3]: https://github.com/jon-bell/bytecode-examples
  [4]: https://wiki.openjdk.org/display/CodeTools/asmtools
  [5]: http://bytebuddy.net/#/
  [6]: https://github.com/qmx/jitescript
  [7]: https://stackoverflow.com/questions/11898566/tutorials-about-javaagents
  [8]: https://www.javacodegeeks.com/2015/09/java-agents.html
  [9]: https://github.com/toptal/jvm-monitoring-agent
  [10]: https://gist.github.com/EntryPointKR/152f089f6f3884047abcd19d39297c9e
  [11]: https://www.infoq.cn/article/Easily-Create-Java-Agents-with-ByteBuddy/
  [12]: https://www.stagemonitor.org/
  [13]: https://docs.oracle.com/javase/specs/jvms/se8/jvms8.pdf
  [14]: https://github.com/waylau/java-virtual-machine-specification
  [15]: https://shipilev.net/jvm/anatomy-quarks/
  [16]: https://www.jcp.org/en/jsr/detail?id=133
  [17]: http://www.cs.umd.edu/~pugh/java/memoryModel/
  [18]: https://gee.cs.oswego.edu/dl/jmm/cookbook.html
  [19]: https://gee.cs.oswego.edu/dl/html/j9mm.html
  [20]: https://book.douban.com/subject/6809987/
  [21]: https://book.douban.com/subject/26740958/
  [22]: https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/
  [23]: https://docs.oracle.com/javase/7/docs/platform/jvmti/jvmti.html
  [24]: https://github.com/headius/bitescript

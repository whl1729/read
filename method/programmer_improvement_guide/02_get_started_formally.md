# 《程序员练级攻略》分析笔记

## 第2章 正式入门

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

介绍具有一定编程基础的新手进一步入门的方法。

### Q3：这一章的大纲是什么

- 编程技能
- 为什么转成 Java 语言？
- 编程工具
- 实践项目

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 编程技能

- [The Key To Accelerating Your Coding Skills][1]: 告诉你如何有效地快速提高自己的编程能力。

- 编程技巧
  - [《代码大全》][2]
  - 好的书和不好的书最大的区别就是，好的书在你不同的阶段来读，你会有不同的收获，而且还会产生更多的深层次的思考！

- 编程语言
  - [《Java 核心技术（卷 1）》][3]：优先推荐。除了让你了解 Java 的语法，它还会让你了解面向对象编程是个什么概念
  - [《Head First Java》][4]：相对基础、难度低。
  - [《Spring in Action》][5]
  - [《Spring Boot 实战》][6]：更新。

- 操作系统
  - [《鸟哥的Linux私房菜》][7]

- 网络协议
  - [MDN HTTP][8]
  - 你需要知道 HTTP 协议的几个关键点：1）HTTP 头，2）HTTP 的请求方法，3）HTTP 的返回码。
  - 还有，HTTP 的 Cookie、缓存、会话，以及链接管理，等等，在 MDN 的这个文档中都有了。
  - 对于 HTTP 协议，你不需要知道所有的东西，你只需要了解这个协议的最关键的那些东西就好了。

- 数据库设计
  - [慕课网在线课程：数据库设计的那些事][9]
  - [《MySQL 必知必会》][10]

- 前端
  - [jQuery][11]
  - [Bootstraop][12]
  - 学习一下如何使用 JavaScript Ajax 请求后端的 API 接口、学习 [JavaScript Promise][13]

- 字符编码
  - [关于字符编码，你所需要知道的（ASCII,Unicode,Utf-8,GB2312…）][14]
  - [The history of Character Encoding][15]
  - [Wikipedia - Character encoding][16]
  - [Awesome Unicode][17]
  - [Awesome Code Points][18]

#### 为什么转成 Java 语言

- Java 是所有语言里面综合实力最强的，这也是为什么几乎所有大型的互联网或是分布式架构基本上都是 Java 技术栈。
  所以，这是一个工业级的编程语言（Python 和 JavaScript 还达不到这样的水准）。

- 像 Python 和 JavaScript 这样的动态语言用着是很爽，但是，只有像 C、C++ 和 Java 这样的静态语言才可以让你真正地进阶。

- 对于一个合格的程序员，掌握几门语言是非常正常的事情。
  - 一方面，这会让你对不同的语言进行比较，让你有更多的思考。
  - 另一方面，这也是一种学习能力的培养。
  - 很多时候，一些程序员只在自己熟悉的技术而不是合适的技术上工作，这其实并不好，这会让你的视野受限，而视野会决定你的高度。

#### 编程工具

- 编程 IDE
  - 传统使用 [Eclipse][19]
  - 推荐使用 [Intellij IDEA][20]
  - 玩时髦使用 [Visual Studio Code][21]

- 版本管理工具
  - 推荐 [《Pro Git（第二版）》][22]
  - 备选 [《猴子都能懂的 Git 入门》][23]
  - [《GitHub and Git 图文教程》][24]
  - [《Git 图文教程及详解》][25]

- 调试前端程序
  - 你需要学会使用 Chrome 调试前端程序，参考资料：[超完整的 Chrome 浏览器客户端调试大全][26]

- 数据库设计工具
  - 你需要学会使用 [MySQL WorkBench][27]

#### 实践项目

这回我们需要设计一个投票系统的项目。

- 业务上的需求如下：
  - 用户只有在登录后，才可以生成投票表单。
  - 投票项可以单选，可以多选。
  - 其它用户投票后显示当前投票结果（但是不能刷票）。
  - 投票有相应的时间，页面上需要出现倒计时。
  - 投票结果需要用不同颜色不同长度的横条，并显示百分比和人数。

- 技术上的需求如下：
  - 这回要用 Java Spring Boot 来实现了，然后，后端不返回任何的 HTML，只返回 JSON 数据给前端。
  - 由前端的 JQuery 来处理并操作相关的 HTML 动态生成在前端展示的页面。
  - 前端的页面还要是响应式的，也就是可以在手机端和电脑端有不同的呈现。 这个可以用 Bootstrap 来完成。

- 如果你有兴趣，还可以挑战以下这些功能。
  - 在微信中，通过微信授权后记录用户信息，以防止刷票。
  - 可以不用刷页面，就可以动态地看到投票结果的变化。
  - Google 一些画图表的 JavaScript 库，然后把图表画得漂亮一些。

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

  [1]: http://blog.thefirehoseproject.com/posts/learn-to-code-and-be-self-reliant
  [2]: https://book.douban.com/subject/1477390/
  [3]: https://book.douban.com/subject/26880667/
  [4]: https://book.douban.com/subject/2000732/
  [5]: https://book.douban.com/subject/26767354/
  [6]: https://book.douban.com/subject/26857423/
  [7]: https://book.douban.com/subject/4889838/
  [8]: https://developer.mozilla.org/zh-CN/docs/Web/HTTP
  [9]: https://www.imooc.com/learn/117
  [10]: https://book.douban.com/subject/3354490/
  [11]: https://jquery.com/
  [12]: https://getbootstrap.com/
  [13]: https://es6.ruanyifeng.com/#docs/promise
  [14]: http://www.imkevinyang.com/2010/06/%E5%85%B3%E4%BA%8E%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81%EF%BC%8C%E4%BD%A0%E6%89%80%E9%9C%80%E8%A6%81%E7%9F%A5%E9%81%93%E7%9A%84.html
  [15]: https://www.hugedomains.com/domain_profile.cfm?d=developerknowhow.com
  [16]: https://en.wikipedia.org/wiki/Character_encoding
  [17]: https://github.com/jagracey/Awesome-Unicode
  [18]: https://github.com/Codepoints/awesome-codepoints
  [19]: https://www.runoob.com/eclipse/eclipse-tutorial.html
  [20]: https://www.runoob.com/w3cnote/intellij-idea-usage.html
  [21]: https://jeasonstudio.gitbooks.io/vscode-cn-doc/content/
  [22]: https://git-scm.com/book/zh/v2/
  [23]: https://backlog.com/git-tutorial/cn/
  [24]: https://github.com/JiapengLi/GitTutorial
  [25]: https://www.jianshu.com/p/1b65ed31da97
  [26]: https://www.shouce.ren/api/view/a/12775
  [27]: https://dev.mysql.com/doc/refman/5.7/en/

# 《程序员练级攻略》分析笔记

## 第1章 零基础启蒙

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

介绍零基础的人入门编程的方法。

### Q3：这一章的大纲是什么

- 编程入门
  - 入门语言 Python
  - 入门 JavaScript
  - 操作系统入门 Linux
  - 编程工具 Visual Studio Code
  - Web 编程入门

- 实践项目

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 编程入门

- 入门教程一：体会编程是什么
  - [《与孩子一起学编程》 ][1]，这本书以 Python 语言教你如何写程序，是一本老少咸宜的编程书。其中会教你编一些小游戏，还会和你讲基本的编程知识，相当不错。
  - 两个在线编程入门的网站：[Codecademy: Learn Python][2] 和 [People Can Program][3]（翻墙打不开），你也可以在这两个网站上学习 Python，只不过是英文的。
  - 然后，你可以到 [CodeAbbey][4] 上去做一些在线编程的小练习。

- 入门教程二：做点实际有用的东西
  - [MDN 的 Web 开发入门][5]：MDN 全称是 Mozilla Developer Network，你可以认为是 Web 方面的官方技术网站。
    - 这个教程会带着你建立一个网站。然后，你可以把你的网页发布在 GitHub 上。

##### 入门语言 Python

- [Python 编程快速上手][6]: 偏文本处理，包括处理 Word、Excel 和 PDF。

- [Python 编程：从入门到实践][7]: 有一些 Web 项目和代码部署方面的内容。

- 如果可能的话，你可以把两本书中的示例都跑一遍。如果你时间有限的话，我推荐你看第二本。

##### 入门 JavaScript

- [MDN JavaScript 教程][8]: 你可以认为这是最权威的 JavaScript 官方教程了，从初级到中级再到高级。
- [W3School JavaScript 教程][9]：这个教程比较偏 Web 方面的编程。
- [JavaScript 全栈教程（廖雪峰）][10]：这是廖雪峰的一个比较偏应用的教程，也是偏 Web 方面的编程，同时包括涉及后端的 Node.js 方面的教程。

##### 操作系统入门 Linux

- [W3CSchool Linux 教程][11]

##### 编程工具 Visual Studio Code

- [Microsoft Visual Studio Code 中文手册][12]

##### Web 编程入门

- 前端基础
  - [MDN HTML 文档][13]
  - [MDN CSS 文档][14]
  - 文档很大，你要学习的并不是所有的东西，而是了解 CSS 和 HTML 是怎么相互作用来展示数据的
  - 然后，不用记忆文档中的内容，这两个文档是用来查找知识的。

- 后端基础
  - 学习 Python 或 Node.js

- 学习要点
  - 学习 HTML 基本语法。
  - 学习 CSS 如何选中 HTML 元素并应用一些基本样式。
  - 学会用 Firefox + Firebug 或 Chrome 查看你觉得很炫的网页结构，并动态修改。
  - 在一台 Linux 机器上配置 LEMP - Ubuntu/Nginx/PHP/MySQL 这个环境。
  - 学习 PHP，让后台 PHP 和前台 HTML 进行数据交互，对服务器响应浏览器请求形成初步认识，并实现一个表单提交和反显的功能。
  - 把 PHP 连接本地或者远程数据库 MySQL（MySQL 和 SQL 现学现用够了）。

#### 实践项目

- 做一个非常简单的 Blog 系统，或是 BBS 系统，需要支持如下功能：
  - 用户登录和注册（不需密码找回）。
  - 用户发贴（不需要支持富文本，只需要支持纯文本）。
  - 用户评论（不需要支持富文本，只需要支持纯文本）。

- 需要关注的几个技术点
  - 用户登录时的密码不应该保存为明文，应该用 MD5+Salt 来保存（关于这个是什么，希望你能自行 Google）。
  - 用户登录后，对于用户自己的贴子可以有“重新编辑”或 “删除”的功能，但是无权编辑或删除其它用户的贴子。
  - 数据库的设计，你需要三张表：用户表、文章表和评论表，它们之间是怎么关联的，你需要学习一下。这里有个 [PHP 的 blog][13] 教你怎么建表，你可以 前往一读

- 如果你有兴趣，你可以顺着这个小项目，研究一下下面这几个事。
  - 图片验证码。
  - 上传图片。
  - 阻止用户在发文章或评论时输入带 HTML 或 JavaScript 的内容。
  - 防范 SQL 注入。参看[PHP 官方文档][14] 或 [微软官方文档][15]，或者你自己 Google 一下。

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

  [1]: https://book.douban.com/subject/5338024/
  [2]: https://www.codecademy.com/learn
  [3]: https://www.peoplecanprogram.com/
  [4]: http://www.codeabbey.com/index/task_list
  [5]: https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web
  [6]: https://book.douban.com/subject/26836700/
  [7]: https://book.douban.com/subject/26829016/
  [8]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript
  [9]: https://www.w3schools.com/js/default.asp
  [10]: https://www.liaoxuefeng.com/wiki/1022910821149312
  [11]: https://www.w3cschool.cn/linux/
  [12]: https://jeasonstudio.gitbooks.io/vscode-cn-doc/content/
  [13]: https://code.tutsplus.com/tutorials/how-to-create-a-phpmysql-powered-forum-from-scratch--net-10188
  [14]: http://php.net/manual/zh/security.database.sql-injection.php
  [15]: https://learn.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008-r2/ms161953(v=sql.105)?redirectedfrom=MSDN

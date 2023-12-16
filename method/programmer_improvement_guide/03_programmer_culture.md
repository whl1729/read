# 《程序员练级攻略》分析笔记

## 第3章 程序员修养

### Q1：这一章的内容属于哪一类别

程序员/方法论。

### Q2：这一章的内容是什么

介绍一名专业程序员需要具备哪些修养及相关的资料。

### Q3：这一章的大纲是什么

- 英文能力
- 问问题的能力
- 写代码的修养
- 安全防范
- 软件工程和上线
- 附录：编程规范
  - 编程语言相关
  - 前端开发相关
  - 移动端相关
  - 开发工具相关

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

- [What are some of the most basic things every programmer should know?][1]
  - Bad architecture causes more problems than bad code.
  - You will spend more time thinking than coding.
  - The best programmers are always building things.
  - There’s always a better way.
  - Code reviews by your peers will make all of you better.
  - Fewer features for better code is always the right answer in the end.
  - If it’s not tested, it doesn’t work.
  - Don’t reinvent the wheel, library code is there to help.
  - Code that’s hard to understand is hard to maintain.
  - Code that’s hard to maintain is next to useless.
  - Always know how your business makes money, that determines who gets paid what.
  - If you want to feel important as a software developer, work at a tech company.

- [Things Every Programmer Should Know][2]

#### 英文能力

- 坚持 Google 英文关键词，而不是在 Google 里搜中文。
- 在 GitHub 上只用英文。用英文写代码注释，写 Code Commit 信息，用英文写 Issue 和 Pull Request，以及用英文写 Wiki。
- 坚持到 YouTube 上每天看 5 分钟的视频。YouTube 上有相关的机器字幕，实在不行就打开字幕。
- 坚持用英文词典而不是中文的。比如：[剑桥英语词典][3] 或是 [Dictionary.com][4] 。你可以安装一个 Chrome 插件 [Google Dictionary][5]。
- 坚持用英文的教材而不是中文的。比如：[BBC 的 Learning English][6]，或是到一些 ESL 网站上看看，如 [ESL: English as a Second Language][7] 上有一些课程。
- 花钱参加一些线上的英文课程，用视频和老外练习。

#### 问问题的能力

- [How To Ask Questions The Smart Way][8]
  - STFW（Search the fxxking web）
  - RTFM（Read the fxxking manual）

- [X-Y Problem][9]
  - 中文版：[X-Y 问题][10]

- [FAQ for StackExchange Site][11]

#### 写代码的修养

- 《重构：改善既有代码的设计》
- 《修改代码的艺术》
- 《代码整洁之道》
- 《程序员的职业素养》

- 作为一个程序员，Code Review 是非常重要的程序员修养。
  - [Code Review Best Practices][12]
  - [How Google Does Code Review][13]
  - [LinkedIn’s Tips for Highly Effective Code Review][14]

- Unit Test
  - [JUnit 5 User Guide][15]
  - [You Still Don’t Know How to Do Unit Testing][16]
  - [Unit Testing Best Practices: JUnit Reference Guide][17]
  - [JUnit Best Practices][18]

#### 安全防范

- [OWASP - Open Web Application Security Project][19]
  - OWASP 是一个开源的、非盈利的全球性安全组织，致力于应用软件的安全研究。
  - 其被视为 Web 应用安全领域的权威参考。

- [OWASP Top Ten][20]
  - [《OWASP Top 10 2017 PDF 中文版》][21]
  - 美国联邦贸易委员会（FTC）强烈建议所有企业需遵循 OWASP 十大 Web 弱点防护守则。

- 安全编程方面的 Guideline
  - [伯克立大学的 Secure Coding Practice Guidelines][22]
  - [卡内基梅隆大学的 SEI CERT Coding Standards][23]

- [Hardening Your HTTP Security Headers][24]: 和 HTTP 相关的安全问题

- [Defensive Programming（防御性编程）][25]
  - [The Art of Defensive Programming][26] （原链接无效了，Google 了新链接，不确定是否正确）
  - 当然，也别太过度了：[Overly defensive programming][27]

#### 软件工程和上线

- 关于测试，推荐两本书。
  - [《完美软件：对软件测试的各种幻想》][28]
    - 这本书重点讨论了与软件测试有关的各种心理问题及其表现与应对方法。
    - 作者首先阐述软件测试之所以如此困难的原因–人的思维不是完美的，而软件测试的最终目的就是发现对改善软件产品和软件开发过程有益的信息，故软件测试是一个信息获取的过程。
  - [《Google 软件测试之道》][29]
    - 描述了测试解决方案，揭示了测试架构是如何设计、实现和运行的，介绍了软件测试工程师的角色；
    - 讲解了技术测试人员应该具有的技术技能；
    - 阐述了测试工程师在产品生命周期中的职责；
    - 讲述了测试管理，并对在 Google 的测试历史上或者主要产品上发挥了重要作用的工程师的访谈。

- 上线前的检查
  - [Server Side checklist][30]
  - [Single Page App Checklist][31]

- [《Monitoring 101》][32]：一篇运维方面的入门文章，告诉你最基本的监控线上运行软件的方法和实践。

#### 附录：编程规范

##### 编程语言相关

- C
  - [NASA C Style][33]
  - [C Coding Standard][34]
  - [C Programming/Structure and style][35]
  - [Linux kernel coding style][36]
  - [GNU Coding Standard][37]

- C++
  - [C++ Core Guidelines][38]：这个文档是各种 C++ 的大拿包括原作者在内在持续讨论更新的和 C++ 语言相关的各种最佳实践。
  - [Google C++ Style Guide][39]

- Go
  - [Effective Go][40]: Go 的语法不复杂，所以，Go 语言的最佳实践只需要看这篇官方文档就够了。

- Java
  - [Code Conventions for the Java™ Programming Language][41]: Java 官方的编程规范。
  - [Google Java Style Guide][42]: Google 的 Java 编码规范。

- JavaScript
  - [JavaScript The Right Way][43]: 一个相对比较容读的 JavaScript 编程规范，其中不但有代码规范，还有设计模式，测试工具，编程框架，游戏引擎……
  - [Google JavaScript Style Guide][44]: Google 公司的 JavaScript 的编码规范，一个非常大而全的编程规范。
  - [Airbnb JavaScript Style Guide][45]: Airbnb 的 JavaScript 编程规范。没 Google 的这么大而全，但是也很丰富了。
  - [jQuery Core Style Guide][46]: jQuery 的代码规范。
  - [JavaScript Clean Code][47]: 前面推荐过的《代码整洁之道》一书中的 JavaScript 的实践 。
  - [JavaScript Style Guide and Coding Convention][48]: 这是 W3Schools 的 JavaScript。
  - [JavaScript Style Guides And Beautifiers][49]
  - [Code Conventions for the JavaScript][50]: Written by Douglas Crockford

- PHP
  - [PHP FIG][51]: PHP 编码规范及标准推荐。
  - [PHP The Right Way][52]: 除了编码规范之外的各种 PHP 的最佳实践，还包括一些设计模式，安全问题，以及服务部署，Docker 虚拟化以及各种资源。
  - [Clean Code PHP][53]: 《代码整洁之道》的 PHP 实践。

- Python
  - [Style Guide for Python Code][54]: Python 官方的编程码规范。
  - [Google Python Style Guide][55]: Google 公司的 Python 编码规范。
  - [The Hitchhiker’s Guide to Python][56]: 这不只是 Python 的编程规范，还是 Python 资源的集散地，强烈推荐。

- Ruby
  - [Ruby Style Guide][57]: Airbnb 公司的 Ruby 编程规范。
  - [Ruby Style Guide][58]

- Rust
  - [Rust Style Guide][59]
  - [Rust 编码规范 中文版][60]

- Scala
  - [Scala Style Guide][61]: Scala 官方的编程规范。
  - [Databricks Scala Guide][62]: Databricks 的 Scala 编程规范。
  - [Scala Best Practices][63]

- Shell
  - [Google Shell Style Guide][106]: Google 的 Shell 脚本编程规范。

- Node.js
  - [npm-coding-style][64]
  - [Microsoft + Node.js Guidelines][65]
  - [Node.js Style Guide][66]

- Mozilla 的编程规范
  - [Mozilla Coding Style Guide][67]: 其中包括 C、C++、Java、Python、JavaScript、Makefile 和 SVG 等编程规范。

##### 前端开发相关

- [CSS Guideline][68]: CSS 容易学，但是不好写，这篇规范会教你如何写出一个健全的、可管理的，并可以扩展的 CSS。
- [Scalable and Modular Architecture for CS][69]: 这是一本教你如何写出可扩展和模块化的 CSS 的电子书，非常不错。
- [Frontend Guideline][70]: 一些和 HTML、CSS、JavaScript 相关的最佳实践。（翻墙打不开）
- [Sass Guideline][71]: Sass 作为 CSS 的补充，其要让 CSS 变得更容易扩展。然而，也变得更灵活，这意味着可以被更容易滥用。这篇“富有主见”的规范值得你一读。
- [Airbnb CSS / Sass Styleguid][72]:  Airbnb 的 CSS/Sass 规范。

- 说了 Sass 就不得不说 LESS，这里有几篇和 LESS 相关的：
  - [LESS Coding Guidelines][73]
  - [LESS Coding Guidelines][74]
  - [LESS coding standard][75]

- [HTML Style Guide][76]: 一个教你如何写出性能更高，结构更好，容易编程和扩展的 HTML 的规范。
- [HTML + CSS Code Guide][77]: 如何写出比较灵活、耐用、可持续改进的 HTML 和 CSS 的规范。
- [CoffeeScript Style Guide][78]: CoffeeScript 的最佳实践和编程规范。
- [Google HTML/CSS Style Guide][79]: Google 的 HTML/CSS 的编程规范。
- [Guidelines for Responsive Web Design][80]: 响应式 Web 设计的规范和最佳实践。
- [U.S. Web Design Standard][81]: 这是美国政府网端要求的一些 UI 交互可视化的一些规范。
- [Front-End Checklist][82]: 一个前端开发的 Checklist，其中包括 HTML、CSS 和 JavaScript，还和图片、字体、SEO、性能相关，还包括一些和安全相关的事项。

##### 移动端相关

- Kotlin
  - [Kotlin Coding Conventions][83]

- Objective-C
  - [Objective-C Style guid][84]: Style guide & coding conventions for Objective-C projects。
  - [Google Objective-C Style Guide][85]
  - [NYTimes Objective-C Style Guide][86]: The Objective-C Style Guide used by The New York Times。

- Swift
  - [API Design Guidelines][87]
  - [Swift][88]: 一个 Swift 的相关编程规范的教程
  - [Swift style guide][89]
  - [Swift Style Guide][90]: LinkedIn 的官方 Swift 编程规范。
  - [Metova’s Swift style guide][91]
  - [Xmartlabs Swift Style Guide][92]: Xmartlabs 的 Swift 编程规范。

##### API 相关

- [HA][93]: 一个简单的 API 规范教程。
- [Microsoft REST API Guideline][94]: 微软的 Rest API 规范。
- [API Design Guide][95]
- [RESTful API Designing guidelines][96]: The best practices。
- [JSON API - Recommendation][97]: JSON 相关的 API 的一些推荐实践。
- [API Security Checklist][98]: API 的安全问题的检查列表。

##### 开发工具相关

- Markdown 相关
  - [Google Markdown Style Guide][99]
  - [Markdown Style Guide][100]

- JSON
  - [Google JSON Style Guide][101]

- Git 相关
  - [Git Style Guide][102]
  - [Few Rules from Git Documentation][103]

- 正则表达式相关
  - [RegexHQ][104]
  - [Learn regex the easy way][105]

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

  [1]: https://www.quora.com/What-are-some-of-the-most-basic-things-every-programmer-should-know
  [2]: https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/index.html
  [3]: https://dictionary.cambridge.org/
  [4]: https://www.dictionary.com/
  [5]: https://chrome.google.com/webstore/detail/google-dictionary-by-goog/mgijmajocgfcbeboacabfgobmjgjcoja
  [6]: http://www.bbc.co.uk/learningenglish/
  [7]: https://www.rong-chang.com/
  [8]: http://www.catb.org/~esr/faqs/smart-questions.html
  [9]: https://xyproblem.info/
  [10]: https://coolshell.cn/articles/10804.html
  [11]: https://meta.stackexchange.com/questions/7931/faq-for-stack-exchange-sites
  [12]: https://blog.palantir.com/code-review-best-practices-19e02780015f
  [13]: https://dzone.com/articles/how-google-does-code-review
  [14]: https://thenewstack.io/linkedin-code-review/
  [15]: https://junit.org/junit5/docs/current/user-guide/
  [16]: https://stackify.com/unit-testing-basics-best-practices/
  [17]: https://dzone.com/articles/unit-testing-best-practices
  [18]: https://dzone.com/articles/unit-testing-best-practices
  [19]: https://owasp.org/
  [20]: https://owasp.org/www-project-top-ten/
  [21]: https://wiki.owasp.org/images/d/dc/OWASP_Top_10_2017_%E4%B8%AD%E6%96%87%E7%89%88v1.3.pdf
  [22]: https://security.berkeley.edu/secure-coding-practice-guidelines
  [23]: https://wiki.sei.cmu.edu/confluence/display/seccode/SEI+CERT+Coding+Standards
  [24]: https://www.keycdn.com/blog/http-security-headers/
  [25]: https://en.wikipedia.org/wiki/Defensive_programming
  [26]: https://www.sas.com/content/dam/SAS/support/en/sas-global-forum-proceedings/2018/1791-2018.pdf
  [27]: https://medium.com/@vcarl/overly-defensive-programming-e7a1b3d234c2
  [28]: https://book.douban.com/subject/4187479/
  [29]: https://book.douban.com/subject/25742200/
  [30]: https://github.com/mtdvio/going-to-production/blob/master/serverside-checklist.md
  [31]: https://github.com/mtdvio/going-to-production/blob/master/spa-checklist.md
  [32]: https://www.datadoghq.com/blog/monitoring-101-collecting-data/
  [33]: https://ntrs.nasa.gov/api/citations/19950022400/downloads/19950022400.pdf
  [34]: https://users.ece.cmu.edu/~eno/coding/CCodingStandard.html
  [35]: https://en.wikibooks.org/wiki/C_Programming/Structure_and_style
  [36]: https://www.kernel.org/doc/html/latest/process/coding-style.html
  [37]: https://www.gnu.org/prep/standards/html_node/Writing-C.html
  [38]: http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines
  [39]: https://google.github.io/styleguide/cppguide.html
  [40]: https://golang.org/doc/effective_go.html
  [41]: https://www.oracle.com/java/technologies/javase/codeconventions-contents.html
  [42]: https://google.github.io/styleguide/javaguide.html
  [43]: http://jstherightway.org/
  [44]: https://google.github.io/styleguide/jsguide.html
  [45]: https://github.com/airbnb/javascript
  [46]: http://contribute.jquery.org/style-guide/js/
  [47]: https://github.com/ryanmcdermott/clean-code-javascript
  [48]: https://addyosmani.com/blog/javascript-style-guides-and-beautifiers/
  [49]: https://www.w3schools.com/js/js_conventions.asp
  [50]: https://www.crockford.com/code.html
  [51]: http://www.php-fig.org/psr/
  [52]: https://phptherightway.com/
  [53]: https://github.com/jupeter/clean-code-php
  [54]: https://peps.python.org/pep-0008/
  [55]: https://google.github.io/styleguide/pyguide.html
  [56]: https://docs.python-guide.org/
  [57]: https://github.com/airbnb/ruby
  [58]: https://github.com/rubocop/ruby-style-guide
  [59]: https://github.com/rust-dev-tools/fmt-rfcs/blob/master/guide/guide.md
  [60]: https://github.com/Rust-Coding-Guidelines/rust-coding-guidelines-zh
  [61]: https://docs.scala-lang.org/style/
  [62]: https://github.com/databricks/scala-style-guide
  [63]: https://github.com/alexandru/scala-best-practices
  [64]: https://doc.codingdict.com/npm-ref/misc/coding-style.html
  [65]: https://github.com/Microsoft/nodejs-guidelines
  [66]: https://github.com/felixge/node-style-guide
  [67]: https://firefox-source-docs.mozilla.org/code-quality/coding-style/index.html
  [68]: https://cssguidelin.es/
  [69]: https://smacss.com/
  [70]: https://github.com/bendc/frontend-guidelines
  [71]: https://sass-guidelin.es/
  [72]: https://github.com/airbnb/css
  [73]: https://gist.github.com/radermacher/f84b24af816111faf0ef
  [74]: https://github.com/odoo/odoo/wiki/LESS-coding-guidelines
  [75]: https://devdocs.magento.com/guides/v2.3/coding-standards/code-standard-less.html
  [76]: https://github.com/marcobiedermann/html-style-guide
  [77]: https://codeguide.co/
  [78]: https://github.com/polarmobile/coffeescript-style-guide
  [79]: https://google.github.io/styleguide/htmlcssguide.html
  [80]: https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/
  [81]: https://designsystem.digital.gov/
  [82]: https://github.com/thedaviddias/Front-End-Checklist
  [83]: https://kotlinlang.org/docs/coding-conventions.html
  [84]: https://github.com/github/objective-c-style-guide
  [85]: https://github.com/google/styleguide/blob/gh-pages/objcguide.md
  [86]: https://github.com/NYTimes/objective-c-style-guide
  [87]: https://www.swift.org/documentation/api-design-guidelines/
  [88]: https://github.com/github/swift-style-guide
  [89]: https://github.com/raywenderlich/swift-style-guide
  [90]: https://github.com/linkedin/swift-style-guide
  [91]: https://github.com/metova/swift-style-guide
  [92]: https://github.com/xmartlabs/Swift-Style-Guide
  [93]: https://stateless.group/hal_specification.html
  [94]: https://github.com/Microsoft/api-guidelines
  [95]: https://apiguide.readthedocs.io/en/latest/
  [96]: https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9
  [97]: https://jsonapi.org/recommendations/
  [98]: https://github.com/shieldfy/API-Security-Checklist
  [99]: https://github.com/google/styleguide/blob/gh-pages/docguide/style.md
  [100]: http://www.cirosantilli.com/markdown-style-guide/
  [101]: https://google.github.io/styleguide/jsoncstyleguide.xml
  [102]: https://github.com/agis/git-style-guide
  [103]: https://github.com/git/git/blob/master/Documentation/CodingGuidelines
  [104]: https://github.com/regexhq
  [105]: https://github.com/ziishaned/learn-regex
  [106]: https://google.github.io/styleguide/shellguide.html

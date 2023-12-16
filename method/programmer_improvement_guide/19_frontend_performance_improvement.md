# 《程序员练级攻略》分析笔记

## 第19章 前端性能优化和框架

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- 前端性能优化
- 前端框架
  - React.js 框架
  - Vue.js 框架

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 前端性能优化

- 图书推荐
  - [Web Performance in Action][1]
    - 这本书目前国内没有卖的。你可以看电子版本，我觉得是一本很不错的书，其中有 CSS、图片、字体、JavaScript 性能调优等。
  - [Designing for Performance][2]
    - 这本在线的电子书很不错，其中讲了很多网页优化的技术和相关的工具，可以让你对整体网页性能优化有所了解。
  - [High Performance JavaScript][3]
    - 这本书能让你了解如何提升各方面的性能，包括代码的加载、运行、DOM 交互、页面生存周期等。
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers][4]
    - 中文版为《高性能网站建设指南：前端工程师技能精髓》。
    - 作者给出了 14 条具体的优化原则，每一条原则都配以范例佐证，并提供了在线支持。
  - Google 的 [Web Fundamentals][5] 里的 [Performance][6] 这一章节也有很多非常不错的知识和经验。

- 最佳实践性的文档
  - [Browser Diet][7]
    - 前端权威性能指南（中文版）。这是一群为大型站点工作的专家们建立的一份前端性能的工作指南。
  - [PageSpeed Insights Rules][8]
    - 谷歌给的一份性能指南和最佳实践。
  - [Best Practices for Speeding Up Your Web Site][9]
    - 雅虎公司给的一份 7 个分类共 35 个最佳实践的文档。

- 性能优化的案例学习网站：[WPO Stats][10]
  - WPO 是 Web Performance Optimization 的缩写，这个网站上有很多很不错的性能优化的案例分享。

- 一些文章和案例
  - [A Simple Performance Comparison of HTTPS, SPDY and HTTP/2][11]
    - 这是一篇比较浏览器的 HTTPS、SPDY 和 HTTP/2 性能的文章，除了比较之外，还可以让你了解一些技术细节。
  - [7 Tips for Faster HTTP/2 Performance][12]
    - 对于 HTTP/2 来说，Nginx 公司给出的 7 个增加其性能的小提示。
  - [Reducing Slack’s memory footprint][13]
    - Slack 团队减少内存使用量的实践。
  - [Pinterest: Driving user growth with performance improvements][14]
    - Pinterest 关于性能调优的一些分享，其中包括了前后端的一些性能调优实践。
  - [10 JavaScript Performance Boosting Tips][15]
    - 10 个提高 JavaScript 运行效率的小提示，挺有用的。
  - [17 Statistics to Sell Web Performance Optimization][16]
    - 这个网页上收集了好些公司的 Web 性能优化的工程分享，都是非常有价值的。
  - [Getting started with the Picture Element][17]
    - 这篇文章讲述了 Responsive 布局所带来的一些负面的问题。
    - 主要是图像适配的问题，其中引出了一篇文章 [Native Responsive Images][18]，值得一读。
  - [Improve Page Load Times With DNS Prefetching][19]
    - 这篇文章教了你一个如何降低 DNS 解析时间的小技术——DNS prefetching。
  - [Jank Busting for Better Rendering Performance][20]
    - 这是一篇 Google I/O 上的分享，关于前端动画渲染性能提升。
  - [JavaScript Memory Profiling][21]
    - 这是一篇谷歌官方教你如何使用 Chrome 的开发工具来分析 JavaScript 内存问题的文章。

- 性能工具
  - [PageSpeed][22]
    - 谷歌有一组 PageSpeed 工具来帮助你分析和优化网站的性能。Google 出品的，质量相当有保证。
  - [YSlow][23]
    - 雅虎的一个网页分析工具。
  - [GTmetrix][24]
    - 是一个将 PageSpeed 和 YSlow 合并起来的一个网页分析工具，并且加上一些 Page load 或是其它的一些分析。
  - [Awesome WPO][25]
    - 在 GitHub 上的这个 Awesome 中，你可以找到更多的性能优化工具和资源。

- 中国的共享库资源
  - [Forget Google and Use These Hosted JavaScript Libraries in China][26]

#### 前端框架

- 框架之间的比较
  - [Angular vs. React vs. Vue: A 2017 comparison][27]
  - [React or Vue: Which JavaScript UI Library Should You Be Using?][28]
  - [ReactJS vs Angular5 vs Vue.js - What to choose in 2018?][29]

#### React.js 框架

- 入门
  - [React 官方教程][30]

- React.js 的基本原理
  - [All the fundamental React.js concepts][31]
    - 这篇文章讲了所有的 React.js 的基本原理。
  - [Learn React Fundamentals and Advanced Patterns][32]
    - 这篇文章中有几个短视频，每个视频不超过 5 分钟，是学习 React 的一个很不错的地方。
  - [Thinking in Reac][33]
    - 这篇文章将引导你完成使用 React 构建可搜索产品数据表的思考过程。

- React.js 的学习重点之一：状态
  - [Common React.js mistakes: Unneeded state][34]
    - React.js 编程的常见错误——不必要的状态。
  - [State is an Anti-Pattern][35]
    - 关于如何做一个不错的组件的思考，很有帮助。
  - [Thinking Statefully][37]
    - 几个很不错的例子让你对声明式有状态的技术有更好的理解。
  - [Tips to learn React + Redux in 2018][38]
    - 传统上，解决 React 的状态问题一般用 Redux。
    - Redux 是一个状态粘合组件，一般来说，我们会用 Redux 来做一些数据状态和其上层 Component 上的同步。
  - "State Architecture Patterns in React" 系列文章
    - [Part 1: A Review][39]
    - [Part 2: The Top-Heavy Architecture, Flux and Performance][40]
    - [Part 3: Articulation Points, zine and An Overall Strategy][41]

- React.js 的学习重点之二：函数式编程
  - [《Professor Frisby’s Mostly Adequate Guide to Functional Programming》][42]（中译版为[《JS 函数式编程指南中文版》][43]）
  - [Master the JavaScript Interview: What is Functional Programming?][44]
  - [The Rise and Fall and Rise of Functional Programming (Composing Software)][45]
  - [Functional UI and Components as Higher Order Functions][46]
  - [Functional JavaScript: Reverse-Engineering the Hype][47]
  - [Some Thoughts on Function Components in React][48]

- React 设计模式
  - [React Pattern][49]
  - [React Higher Order Components in depth][50]
  - [Presentational and Container Components][51]
  - [Controlled and uncontrolled form inputs in React don’t have to be complicated][52]
  - [Function as Child Components][53]
  - [Writing Scalable React Apps with the Component Folder Pattern][54]
  - [Reusable Web Application Strategies][55]
  - [Characteristics of an Ideal React Architecture][56]

- React 实践和经验
  - [9 things every React.js beginner should know][57]
  - [Best practices for building large React applications][58]
  - [Clean Code vs. Dirty Code: React Best Practices][59]
  - [How to become a more productive React Developer][60]
  - [8 Key React Component Decisions][61]

- React 的资源列表
  - [Awesome React][62]
    - 这是一些 React 相关资源的列表，很大很全。
  - [React/Redux Links][63]
    - 这也是 React 相关的资源列表，与上面不一样的是，这个列表主要收集了大量的文章，其中讲述了很多 React 知识和技术，比上面的列表好很多。
  - [React Rocks][64]
    - 这个网站主要收集各种 React 的组件示例，可以让你大开眼界。

#### Vue.js 框架

- 初步了解 Vue 的一些文章
  - [Why 43% of Front-End Developers want to learn Vue.js][65]
    - 你可以看出 Vue 和 React 的编程方式是大相径庭的，符合传统的前端开发的思维方式。
  - [Replacing jQuery With Vue.js: No Build Step Necessary][66]
    - 从 jQuery 是可以平滑过渡到 Vue 的。
  - [10 things I love about Vue][67]
    - 了解 Vue 的一些比较优秀的特性。

- 2018 年对尤雨溪的采访
  - [Vue on 2018 - Interview with Evan You][68]

- Vue 入门
  - [Vue 官方文档][69]（[中文版][70]）
  - [Vue.js screencasts][71]
  - [新手向：Vue 2.0 的建议学习顺序][72]

- Vue 学习资料
  - [How not to Vue][73]
    - 任何技术都有坑，了解 Vue 的短板，你就能扬长避短，就能用得更好。
  - [Vue.js Component Communication Patterns][74]
  - [4 AJAX Patterns For Vue.js Apps][75]
  - [How To (Safely) Use A jQuery Plugin With Vue.js][76]
  - [7 Ways To Define A Component Template in Vue.js][77]
  - [Use Any Javascript Library With Vue.js][78]
  - [Dynamic and async components made easy with Vue.js][79]

- Vue 资源列表
  - [Awesome Vue][80]

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

  [1]: https://www.manning.com/books/web-performance-in-action
  [2]: https://designingforperformance.com/
  [3]: https://book.douban.com/subject/5362856/
  [4]: https://book.douban.com/subject/26411563/
  [5]: https://web.dev/
  [6]: https://web.dev/why-speed-matters/
  [7]: https://browserdiet.com/zh/
  [8]: https://developers.google.com/speed/docs/insights/rules
  [9]: https://developer.yahoo.com/performance/rules.html
  [10]: https://wpostats.com/
  [11]: http://blog.httpwatch.com/2015/01/16/a-simple-performance-comparison-of-https-spdy-and-http2/
  [12]: https://www.nginx.com/blog/7-tips-for-faster-http2-performance/
  [13]: https://slack.engineering/reducing-slacks-memory-footprint/
  [14]: https://medium.com/pinterest-engineering/driving-user-growth-with-performance-improvements-cfc50dafadd7
  [15]: http://jonraasch.com/blog/10-javascript-performance-boosting-tips-from-nicholas-zakas
  [16]: https://www.guypo.com/17-statistics-to-sell-web-performance-optimization
  [17]: https://deanhume.com/getting-started-with-the-picture-element/
  [18]: https://dev.opera.com/articles/native-responsive-images/
  [19]: https://deanhume.com/improve-page-load-times-with-dns-prefetching/
  [20]: https://web.dev/speed-rendering/
  [21]: https://developer.chrome.com/docs/devtools/
  [22]: https://developers.google.com/speed
  [23]: https://github.com/marcelduran/yslow
  [24]: https://gtmetrix.com/
  [25]: https://github.com/davidsonfellipe/awesome-wpo
  [26]: http://chineseseoshifu.com/blog/china-hosted-javascript-libraries-jquery-dojo-boostrap.html
  [27]: https://medium.com/pixelpassion/angular-vs-react-vs-vue-a-2017-comparison-c5c52d620176
  [28]: https://medium.com/js-dojo/react-or-vue-which-javascript-ui-library-should-you-be-using-543a383608d
  [29]: https://medium.com/techmagic/reactjs-vs-angular5-vs-vue-js-what-to-choose-in-2018-b91e028fa91d
  [30]: https://reactjs.org/tutorial/tutorial.html
  [31]: https://www.freecodecamp.org/news/all-the-fundamental-react-js-concepts-jammed-into-this-single-medium-article-c83f9b53eac2
  [32]: https://kentcdodds.com/blog/learn-react-fundamentals-and-advanced-patterns
  [33]: https://reactjs.org/docs/thinking-in-react.html
  [34]: https://reactkungfu.com/2015/09/common-react-dot-js-mistakes-unneeded-state/
  [35]: https://www.reddit.com/r/reactjs/comments/3bjdoe/state_is_an_antipattern/
  [37]: https://daveceddia.com/thinking-statefully/
  [38]: https://www.robinwieruch.de/tips-to-learn-react-redux/
  [39]: https://medium.com/@skylernelson_64801/state-architecture-patterns-in-react-a-review-df02c1e193c6
  [40]: https://medium.com/@skylernelson_64801/state-architecture-patterns-in-react-part-2-the-top-heavy-architecture-flux-and-performance-a388b928ce89
  [41]: https://medium.com/@skylernelson_64801/state-architecture-patterns-in-react-part-3-articulation-points-zine-and-an-overall-strategy-cf076f906391
  [42]: https://github.com/MostlyAdequate/mostly-adequate-guide
  [43]: https://jigsawye.gitbooks.io/mostly-adequate-guide/content/
  [44]: https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0
  [45]: https://medium.com/javascript-scene/the-rise-and-fall-and-rise-of-functional-programming-composable-software-c2d91b424c8c
  [46]: https://blog.risingstack.com/functional-ui-and-components-as-higher-order-functions/
  [47]: http://banderson.github.io/functional-js-reverse-engineering-the-hype/#/
  [48]: https://medium.com/javascript-inside/some-thoughts-on-function-components-in-react-cb2938686bc7
  [49]: https://reactpatterns.com/
  [50]: https://medium.com/@franleplant/react-higher-order-components-in-depth-cf9032ee6c3e
  [51]: https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0
  [52]: https://goshacmd.com/controlled-vs-uncontrolled-inputs-react/
  [53]: https://medium.com/merrickchristensen/function-as-child-components-5f3920a9ace9
  [54]: https://medium.com/styled-components/component-folder-pattern-ee42df37ec68
  [55]: https://www.freecodecamp.org/news/reusable-web-application-strategies-d51517ea68c8
  [56]: https://medium.com/@robftw/characteristics-of-an-ideal-react-architecture-883b9b92be0b
  [57]: https://camjackson.net/post/9-things-every-reactjs-beginner-should-know
  [58]: https://engineering.sift.com/best-practices-for-building-large-react-applications/
  [59]: https://americanexpress.io/clean-code-dirty-code/
  [60]: https://dev.to/jakoblind/how-to-become-a-more-productive-react-developer
  [61]: https://www.freecodecamp.org/news/8-key-react-component-decisions-cc965db11594
  [62]: https://github.com/enaqx/awesome-react
  [63]: https://github.com/markerikson/react-redux-links
  [64]: https://react.rocks/
  [65]: https://medium.com/vue-mastery/why-43-of-front-end-developers-want-to-learn-vue-js-7f23348bc5be
  [66]: https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/
  [67]: https://medium.com/@dalaidunc/10-things-i-love-about-vue-505886ddaff2
  [68]: https://blog.hackages.io/https-blog-hackages-io-evanyoubhack2017-cc5559806157
  [69]: https://vuejs.org/guide/introduction.html
  [70]: https://v2.cn.vuejs.org/
  [71]: https://laracasts.com/series/learn-vue-2-step-by-step
  [72]: https://zhuanlan.zhihu.com/p/23134551
  [73]: https://itnext.io/how-not-to-vue-18f16fe620b5
  [74]: https://www.digitalocean.com/community/tutorials/vuejs-component-communication
  [75]: https://medium.com/js-dojo/4-ajax-patterns-for-vue-js-apps-add915fc9168
  [76]: https://vuejsdevelopers.com/2017/05/20/vue-js-safely-jquery-plugin/
  [77]: https://vuejsdevelopers.com/2017/03/24/vue-js-component-templates/
  [78]: https://vuejsdevelopers.com/2017/04/22/vue-js-libraries-plugins/
  [79]: https://dev.to/lobo_tuerto/dynamic-and-async-components-made-easy-with-vuejs-579j
  [80]: https://github.com/vuejs/awesome-vue

# 《程序员练级攻略》分析笔记

## 第18章 前端基础和底层原理

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- HTML5
- CSS
- JavaScript
- 浏览器原理
- 网络协议

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

- 前端的三个最基本的东西 HTML 5、CSS 3 和 JavaScript（ES6）是必须要学好的。

- 前端需要掌握的基础知识和基本原理
  - JavaScript 的核心原理。 这里我会给出好些网上很不错的讲 JavaScript 的原理的文章或图书，你一定要学好语言的特性，并且详细了解其中的各种坑。
  - 浏览器的工作原理。这也是一块硬骨头，我觉得这是前端程序员需要了解和明白的关键知识点，不然，你将无法深入下去。
  - 网络协议 HTTP。也是要着重了解的，尤其是 HTTP/2，还有 HTTP 的几种请求方式：短连接、长连接、Stream 连接、WebSocket 连接。
  - 前端性能调优。有了以上的这些基础后，你就可以进入前端性能调优的主题了，我相信你可以很容易上手各种性能调优技术的。
  - 框架学习。我只给了 React 和 Vue 两个框架。
    - 就这两个框架来说，Virtual DOM 技术是其底层技术，组件化是其思想，管理组件的状态是其重点。
    - 而对于 React 来说，函数式编程又是其编程思想，所以，这些基础技术都是你需要好好研究和学习的。
  - UI 设计。设计也是前端需要做的一个事，比如像 Google 的 Material UI，或是比较流行的 Atomic Design 等应该是前端工程师需要学习的。

#### HTML5

- 书籍推荐
  - [HTML 5 权威指南][1]
    - 本书面向初学者和中等水平 Web 开发人员，是牢固掌握 HTML 5、CSS 3 和 JavaScript 的必读之作。
    - 书看起来比较厚，是因为里面的代码很多。
  - [HTML 5 Canvas 核心技术][2]
    - 如果你要做 HTML 5 游戏的话，这本书必读。

- SVG、Canvas 和 WebGL
  - 这三个对应于矢量图、位图和 3D 图的渲染来说，给前端开发带来了重武器，很多 HTML5 小游戏也因此蓬勃发展。
  - 学习这三个技术，我个人觉得最好的地方是 MDN。
    - [SVG: Scalable Vector Graphics][3]
    - [Canvas API][4]
    - [The WebGL API: 2D and 3D graphics for the web][5]

- 资料列表
  - [Awesome HTML5][6]
  - [Awesome SVG][7]
  - [Awesome Canvas][8]
  - [Awesome WebGL][9]

#### CSS

- CSS 的学习方法
  - 绝大多数觉得难的，一方面是文档没读透，另一方面是浏览器支持的标准不一致。
  - 只要你仔细读一下文档，CSS 并不难学。

- [MDN Web Doc - CSS][10]
  - CSS 的在线学习文档

- [LESS][11] 和 [SaSS][12]
  - 你需要学会使用 LESS 和 SaSS 这两个 CSS 预处理工具，可以帮你提高很多效率。

- CSS 的书写规范
  - [Principles of writing consistent, idiomatic CSS][13]
  - [Opinionated CSS styleguide for scalable applications][14]
  - [Google HTML/CSS Style Guide][15]

- CSS Framework
  - 最著名的是 Twitter 公司的 [Bootstrap][16]
  - 主打清新 UI 的 [Semantic UI][17]
  - 主打响应式界面的 [Foundation][18]
  - 基于 Flexbox 的 [Bulma][19]

- 几个 Reset 或标准化的 CSS 库
  - [Normalize][20]
  - [MiniRest.css][21]
  - [sanitize.css][22]
  - [unstyle.css][23]

- CSS 框架资源列表
  - [Awesome CSS Frameworks][24]

- 几个公司的 CSS 相关实践
  - [CodePen’s CSS][25]
  - [Github 的 CSS][26]
  - [Medium’s CSS is actually pretty f***ing good][27]
  - [CSS at BBC Sport][28]
  - [Refining The Way We Structure Our CSS At Trello][29]

- 可以写出可扩展的 CSS 的阅读列表
  - [A Scalable CSS Reading List][30]

#### JavaScript

- [JavaScript: The Good Parts][31]
  - 中文翻译版为《JavaScript 语言精粹》。
  - 这是一本介绍 JavaScript 语言本质的权威图书，值得任何正在或准备从事 JavaScript 开发的人阅读，并且需要反复阅读。

- [Secrets of the JavaScript Ninja][32]
  - 中文翻译版为《JavaScript 忍者秘籍》
  - 本书是 jQuery 库创始人编写的一本深入剖析 JavaScript 语言的书。

- [Effective JavaScript][33]
  - Ecma 的 JavaScript 标准化委员会著名专家撰写
  - 作者凭借多年标准化委员会工作和实践经验，深刻辨析 JavaScript 的内部运作机制、特性、陷阱和编程最佳实践，将它们高度浓缩为极具实践指导意义的 68 条精华建议。

- ES6 的学习手册
  - [ES6 in Dept][34]
    - InfoQ 上有相关的中文版 - [ES6 深入浅出][35]。
  - [阮一峰翻译的 ES6 的教程][37]。
  - [ECMAScript 6 Tools][38]
    - 这是一堆 ES6 工具的列表，可以帮助你提高开发效率。
  - [Modern JS Cheatsheet][39]
    - 这个 Cheatsheet 在 GitHub 上有 1 万 6 千颗星，你就可见其影响力了。

- [《You Don’t Know JS 系列》 ][40]

- 编程范式相关的文章
  - [Glossary of Modern JavaScript Concepts: Part 1][47]
    - 首先推荐这篇文章，其中收集了一些编程范式方面的内容，比如纯函数、状态、可变性和不可变性、指令型语言和声明式语言、函数式编程、响应式编程、函数式响应编程。
  - [Glossary of Modern JavaScript Concepts: Part 2][48]
    - 在第二部分中主要讨论了作用域和闭包，数据流，变更检测，组件化……

- 德米特里·索什尼科夫（Dmitry Soshnikov）个人网站上三篇讲 JavaScript 内在的文章
  - [JavaScript. The Core: 2nd Edition][49]
  - [JavaScript. The Core (older ES3 version)][50]
  - [JS scope: static, dynamic, and runtime-augmented][51]

- SessionStake 的 CEO 写的 “How JavaScript Works” 系列文章
  - [An overview of the engine, the runtime, and the call stack][52]
  - [Inside the V8 engine + 5 tips on how to write optimized code][53]：了解 V8 引擎。
    这里，也推荐 [Understanding V8’s Bytecode][54] 这篇文章可以让你了解 V8 引擎的底层字节码。
  - [Memory management + how to handle 4 common memory leaks][55]：内存管理和 4 种常见的内存泄露问题。
  - [Event loop and the rise of Async programming + 5 ways to better coding with async/await][56]：Event Loop 和异步编程。
  - [Deep dive into WebSockets and HTTP/2 with SSE + how to pick the right path][57]：WebSocket 和 HTTP/2。
  - [A comparison with WebAssembly + why in certain cases it’s better to use it over JavaScript][58]：JavaScript 内在原理。
  - [The building blocks of Web Workers + 5 cases when you should use them][59]：Web Workers 技术。
  - [Service Workers, their lifecycle and use cases][60]：Service Worker 技术。
  - [The mechanics of Web Push Notifications][61]：Web 端 Push 通知技术。
  - [Tracking changes in the DOM using MutationObserver][62]：Mutation Observer 技术。
  - [The rendering engine and tips to optimize its performance][63]：渲染引擎和性能优化。
  - [Inside the Networking Layer + How to Optimize Its Performance and Security][64]：网络性能和安全相关。
  - [Under the hood of CSS and JS animations + how to optimize their performance][65]：CSS 和 JavaScript 动画性能优化。

- Google Chrome 工程经理 阿迪·奥斯马尼（Addy Osmani） 的几篇 JavaScript 性能相关的文章
  - [The Cost Of JavaScript][66]
  - [JavaScript Start-up Performance][67]

- 其它与 JavaScript 相关的资源
  - [JavScript has Unicode Problem][68]
    - 这是一篇很有价值的 JavaScript 处理 Unicode 的文章。
  - [JavaScript Algorithms][69]
    - 用 JavaScript 实现的各种基础算法库。
  - [JavaScript 30 秒代码][70]
    - 一堆你可以在 30 秒内看懂各种有用的 JavaScript 的代码，在 GitHub 上有 2 万颗星了。
  - [What the f*ck JavaScript][71]
    - 一堆 JavaScript 搞笑和比较 tricky 的样例。
  - [Airbnb JavaScript Style Guide][72]
    - Airbnb 的 JavaScript 的代码规范，GitHub 上有 7 万多颗星。
  - [JavaScript Patterns for 2017][73]
    - YouTube 上的一个 JavaScript 模式分享，值得一看。

#### 浏览器原理

- 浏览器的工作原理
  - [《How browsers work》][74]
  - [《How Browsers Work: Behind the scenes of modern web browsers》][75]
    - 重新整理的版本。这篇文章非常非常长，所以，你要有耐心看完。
  - [《浏览器的渲染原理简介》][76]
    - 酷壳上的文章
  - [一个 PPT][77]

- Virtual DOM
  - Virtual DOM 是 React 的一个非常核心的技术细节，它也是前端渲染和性能的关键技术。
  - [How to write your own Virtual DOM][78]
  - [Write your Virtual DOM 2: Props & Events][79]
  - [How Virtual-DOM and diffing works in React][80]
  - [The Inner Workings Of Virtual DOM][81]
  - [深度剖析：如何实现一个 Virtual DOM 算法][82]

- 两个 Vitual-DOM 实现
  - [Matt-Esch/Virtual-DO][83]
  - [MMaquette][84]

#### 网络协议

- [High Performance Browser Networking ][85]
  - 本书是谷歌公司高性能团队核心成员的权威之作，堪称实战经验与规范解读完美结合的产物。
  - 本书目标是涵盖 Web 开发者技术体系中应该掌握的所有网络及性能优化知识。

- [HTTP/2][86] 学习资源
  - [Gitbook - HTTP/2 详解][87]
  - [http2 explained（中译版）][88]
  - [HTTP/2 for a Faster Web][89]
  - [Nginx HTTP/2 白皮书][90]

- HTTP/2 的两个 RFC
  - [RFC 7540 - Hypertext Transfer Protocol Version 2 (HTTP/2)][91]：HTTP/2 的协议本身。
  - [RFC 7541 - HPACK: Header Compression for HTTP/2][92]：HTTP/2 的压缩算法。

- 新的 HTML5 支持 [WebSocket][93]，所以，这也是你要学的一个重要协议。
  - [HTML5 WebSocket: A Quantum Leap in Scalability for the Web][94] （链接失效了）
    - 这篇文章比较了 HTTP 的几种链接方式，Polling、Long Polling 和 Streaming，并引入了终级解决方案 WebSocket。
    - 你知道的，了解一个技术的缘由是非常重要的。
  - StackOverflow[: My Understanding of HTTP Polling, Long Polling, HTTP Streaming and WebSockets][95]
    - 这是 StackOverflow 上的一个 HTTP 各种链接方式的比较，也可以让你有所认识。
  - [An introduction to Websockets][96]：一个 WebSocket 的简单教程。
  - [Awesome Websockets][97]：GitHub 的 Awesome 资源列表。

- 一些和 WebSocket 相关的想法，可以开阔你的思路
  - [Introducing WebSockets: Bringing Sockets to the Web][98]
  - [Websockets 101][99]
  - [Real-Time Web by Paul Banks][100]
  - [Are WebSockets the future?][101]

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

  [1]: https://book.douban.com/subject/25786074/
  [2]: https://book.douban.com/subject/24533314/
  [3]: https://developer.mozilla.org/en-US/docs/Web/SVG
  [4]: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API?retiredLocale=kab
  [5]: https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API
  [6]: https://github.com/diegocard/awesome-html5
  [7]: https://github.com/willianjusten/awesome-svg
  [8]: https://github.com/raphamorim/awesome-canvas
  [9]: https://github.com/sjfricke/awesome-webgl
  [10]: https://developer.mozilla.org/zh-CN/docs/Web/CSS
  [11]: https://lesscss.org/
  [12]: http://sass-lang.com/
  [13]: https://github.com/necolas/idiomatic-css
  [14]: https://github.com/grvcoelho/css-styleguide
  [15]: https://google.github.io/styleguide/htmlcssguide.html
  [16]: https://getbootstrap.com/
  [17]: https://semantic-ui.com/
  [18]: https://get.foundation/
  [19]: https://bulma.io/
  [20]: https://github.com/necolas/normalize.css
  [21]: https://github.com/jgthms/minireset.css
  [22]: https://github.com/csstools/sanitize.css
  [23]: https://github.com/Martin-Pitt/css-unstyle
  [24]: https://github.com/troxler/awesome-css-frameworks
  [25]: https://codepen.io/chriscoyier/post/codepens-css
  [26]: https://markdotto.com/2014/07/23/githubs-css/
  [27]: https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06
  [28]: https://medium.com/bbc-design-engineering/css-at-bbc-sport-part-1-bab546184e66
  [29]: https://blog.trello.com/refining-the-way-we-structure-our-css-at-trello
  [30]: https://github.com/davidtheclark/scalable-css-reading-list
  [31]: https://book.douban.com/subject/11874748/
  [32]: https://book.douban.com/subject/26638316/
  [33]: https://book.douban.com/subject/25786138/
  [34]: https://hacks.mozilla.org/category/es6-in-depth/
  [35]: https://www.infoq.cn/minibook/es6-in-depth
  [37]: https://es6.ruanyifeng.com/
  [38]: https://github.com/addyosmani/es6-tools
  [39]: https://mbeaudru.github.io/modern-js-cheatsheet/
  [40]: https://github.com/getify/You-Dont-Know-JS
  [47]: https://auth0.com/blog/glossary-of-modern-javascript-concepts/
  [48]: https://auth0.com/blog/glossary-of-modern-javascript-concepts-part-2/
  [49]: http://dmitrysoshnikov.com/ecmascript/javascript-the-core-2nd-edition/
  [50]: http://dmitrysoshnikov.com/ecmascript/javascript-the-core/
  [51]: https://codeburst.io/js-scope-static-dynamic-and-runtime-augmented-5abfee6223fe
  [52]: https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf?gi=164636574ee9
  [53]: https://blog.sessionstack.com/how-javascript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e
  [54]: https://medium.com/dailyjs/understanding-v8s-bytecode-317d46c94775
  [55]: https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec
  [56]: https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5
  [57]: https://blog.sessionstack.com/how-javascript-works-deep-dive-into-websockets-and-http-2-with-sse-how-to-pick-the-right-path-584e6b8e3bf7
  [58]: https://blog.sessionstack.com/how-javascript-works-a-comparison-with-webassembly-why-in-certain-cases-its-better-to-use-it-d80945172d79
  [59]: https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a
  [60]: https://blog.sessionstack.com/how-javascript-works-service-workers-their-life-cycle-and-use-cases-52b19ad98b58 
  [61]: https://blog.sessionstack.com/how-javascript-works-the-mechanics-of-web-push-notifications-290176c5c55d
  [62]: https://blog.sessionstack.com/how-javascript-works-tracking-changes-in-the-dom-using-mutationobserver-86adc7446401
  [63]: https://blog.sessionstack.com/how-javascript-works-the-rendering-engine-and-tips-to-optimize-its-performance-7b95553baeda
  [64]: https://blog.sessionstack.com/how-javascript-works-inside-the-networking-layer-how-to-optimize-its-performance-and-security-f71b7414d34c
  [65]: https://blog.sessionstack.com/how-javascript-works-under-the-hood-of-css-and-js-animations-how-to-optimize-their-performance-db0e79586216
  [66]: https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e
  [67]: https://medium.com/reloading/javascript-start-up-performance-69200f43b201
  [68]: https://mathiasbynens.be/notes/javascript-unicode
  [69]: https://mgechev.github.io/javascript-algorithms/index.html
  [70]: https://github.com/30-seconds/30-seconds-of-code
  [71]: https://github.com/denysdovhan/wtfjs
  [72]: https://github.com/airbnb/javascript
  [73]: https://www.youtube.com/watch?v=hO7mzO83N1Q
  [74]: http://taligarsiel.com/Projects/howbrowserswork1.htm
  [75]: https://web.dev/howbrowserswork
  [76]: https://coolshell.cn/articles/9666.html
  [77]: http://arvindr21.github.io/howBrowserWorks/#/
  [78]: https://medium.com/@deathmood/how-to-write-your-own-virtual-dom-ee74acc13060
  [79]: https://medium.com/@deathmood/write-your-virtual-dom-2-props-events-a957608f5c76
  [80]: https://medium.com/@gethylgeorge/how-virtual-dom-and-diffing-works-in-react-6fc805f9f84e
  [81]: https://rajaraodv.medium.com/the-inner-workings-of-virtual-dom-666ee7ad47cf
  [82]: https://github.com/livoras/blog/issues/13
  [83]: https://github.com/Matt-Esch/virtual-dom
  [84]: https://maquettejs.org/
  [85]: https://book.douban.com/subject/25856314/
  [86]: https://en.wikipedia.org/wiki/HTTP/2
  [87]: https://http2-explained.haxx.se/
  [88]: https://http2-explained.haxx.se/zh
  [89]: https://cascadingmedia.com/insites/2015/03/http-2.html
  [90]: https://www.nginx.com/wp-content/uploads/2015/09/NGINX_HTTP2_White_Paper_v4.pdf
  [91]: https://httpwg.org/specs/rfc7540.html
  [92]: https://httpwg.org/specs/rfc7541.html
  [93]: https://en.wikipedia.org/wiki/WebSocket
  [94]: http://www.websocket.org/quantum.html
  [95]: https://stackoverflow.com/questions/12555043/my-understanding-of-http-polling-long-polling-http-streaming-and-websockets
  [96]: https://blog.teamtreehouse.com/an-introduction-to-websockets
  [97]: https://github.com/facundofarias/awesome-websockets
  [98]: https://web.dev/websockets-basics/
  [99]: https://lucumr.pocoo.org/2012/9/24/websockets-101/
  [100]: https://banksco.de/p/state-of-realtime-web-2016.html
  [101]: https://samsaffron.com/archive/2015/12/29/websockets-caution-required

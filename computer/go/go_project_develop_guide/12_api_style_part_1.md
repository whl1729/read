# 《Go 语言项目开发实战》分析笔记

## 第12章 API 风格（上）：如何设计 RESTful API？

### Q1：这一章的内容属于哪一类别？

计算机/软件设计。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- RESTful API 介绍
- RESTful API 设计原则
  - URI 设计
  - REST 资源操作映射为 HTTP 方法
  - 统一的返回格式
  - API 版本管理
  - API 命令
  - 统一分页/过滤/排序/搜索功能
  - 域名
- REST 示例
- 总结

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### RESTful API 介绍

- REST
  - REpresentational State Transfer，表现层状态转移
  - 出自：[《Architectural Styles and the Design of Network-based Software Architectures》][1]
  - REST 本身并没有创造新的技术、组件或服务
  - 它只是一种软件架构风格，是一组架构约束条件和原则，而不是技术框架

- REST 规范
  - REST 规范把所有内容都视为资源，也就是说网络上一切皆资源。
  - REST 架构对资源的操作包括获取、创建、修改和删除，这些操作正好对应 HTTP 协议提供的 GET、POST、PUT 和 DELETE 方法。
  - 由于 REST 天生和 HTTP 协议相辅相成，因此 HTTP 协议已经成了实现 RESTful API 事实上的标准

- REST 核心特点
  - 以资源 (resource) 为中心，所有的东西都抽象成资源，所有的行为都应该是在资源上的 CRUD 操作。
    - 资源对应着面向对象范式里的对象，面向对象范式以对象为中心。
    - 资源使用 URI 标识，每个资源实例都有一个唯一的 URI 标识。
      例如，如果我们有一个用户，用户名是 admin，那么它的 URI 标识就可以是 /users/admin。
  - 资源是有状态的，使用 JSON/XML 等在 HTTP Body 里表征资源的状态。
  - 客户端通过四个 HTTP 动词，对服务器端资源进行操作，实现「表现层状态转化」。
  - 无状态，这里的无状态是指每个 RESTful API 请求都包含了所有足够完成本次操作的信息，服务器端无须保持 session。
    无状态对于服务端的弹性扩容是很重要的。

- RSSTful API
  - REST 有一系列规范，满足这些规范的 API 均可称为 RESTful API

#### RESTful API 设计原则

##### URI 设计

- 资源名使用名词而不是动词，并且用名词复数表示。
  - 资源分为 Collection 和 Member 两种
  - Collection：一堆资源的集合。例如我们系统里有很多用户（User）, 这些用户的集合就是 Collection。
    Collection 的 URI 标识应该是 「域名/资源名复数」, 例如 `https:// iam.api.marmotedu.com/users`。
  - Member：单个特定资源。例如系统中特定名字的用户，就是 Collection 里的一个 Member。
    Member 的 URI 标识应该是 「域名/资源名复数/资源名称」, 例如 `https:// iam.api.marmotedu/users/admin`。

- URI 结尾不应包含/。

- URI 中不能出现下划线 `_`，必须用中杠线 -代替（有些人推荐用`_`，有些人推荐用 -，统一使用一种格式即可，我比较推荐用 -）。

- URI 路径用小写，不要用大写。

- 避免层级过深的 URI。超过 2 层的资源嵌套会很乱，建议将其他资源转化为?参数，比如：

  ```bash
  /schools/tsinghua/classes/rooma/students/zhang # 不推荐
  /students?school=qinghua&class=rooma # 推荐
  ```

- 当有些操作不能很好地映射为一个 REST 资源时
  - 将一个操作变成资源的一个属性，比如想在系统中暂时禁用某个用户，可以这么设计 URI：/users/zhangsan?active=false。
  - 将操作当作是一个资源的嵌套资源，比如一个 GitHub 的加星操作（如下所示）。
  - 如果以上都不能解决问题，有时可以打破这类规范。比如登录操作，登录不属于任何一个资源，URI 可以设计为：/login。

  ```bash
  PUT /gists/:id/star # github star action
  DELETE /gists/:id/star # github unstar action
  ```

- 遇事不决可查看
  - [《GitHub 标准 RESTful API》][2]
  - [Google API Design Guide][3]

##### REST 资源操作映射为 HTTP 方法

- 基本上 RESTful API 都是使用 HTTP 协议原生的 GET、PUT、POST、DELETE 来标识对资源的 CRUD 操作。

- GET 返回的结果，要尽量可用于 PUT、POST 操作中。
  - 例如，用 GET 方法获得了一个 user 的信息，调用者修改 user 的邮件，然后将此结果再用 PUT 方法更新。这要求 GET、PUT、POST 操作的资源属性是一致的。

- 如果对资源进行状态 / 属性变更，要用 PUT 方法，POST 方法仅用来创建或者批量删除这两种场景。

- 批量删除的三种方式
  - 发起多个 DELETE 请求。
  - 操作路径中带多个 id，id 之间用分隔符分隔, 例如：DELETE /users?ids=1,2,3。（推荐）
  - 直接使用 POST 方式来批量删除，body 中传入需要删除的资源列表。

##### 统一的返回格式

- 一个系统的 RESTful API 会向外界开放多个资源的接口，每个接口的返回格式要保持一致。

- 另外，每个接口都会返回成功和失败两种消息，这两种消息的格式也要保持一致。
  - 不然，客户端代码要适配不同接口的返回格式，每个返回格式又要适配成功和失败两种消息格式，会大大增加用户的学习和使用成本。

##### API 版本管理

- API 版本有不同的标识方法，在 RESTful API 开发中，通常将版本标识放在如下 3 个位置：
  - URL 中，比如/v1/users。（很直观，推荐）
  - HTTP Header 中，比如Accept: vnd.example-com.foo+json; version=1.0。
  - Form 参数中，比如/users?version=v1。

##### API 命名

- API 的3种命令方式
  - 驼峰命名法 (serverAddress)
  - 蛇形命名法 (server_address)
  - 脊柱命名法 (server-address) （不需切换输入法，推荐）

##### 统一分页/过滤/排序/搜索功能

- 分页
  - 在列出一个 Collection 下所有的 Member 时，应该提供分页功能，例如/users?offset=0&limit=20（limit，指定返回记录的数量；offset，指定返回记录的开始位置）。
  - 引入分页功能可以减少 API 响应的延时，同时可以避免返回太多条目，导致服务器 / 客户端响应特别慢，甚至导致服务器 / 客户端 crash 的情况。

- 过滤
  - 如果用户不需要一个资源的全部状态属性，可以在 URI 参数里指定返回哪些属性，例如/users?fields=email,username,address。

- 排序
  - 用户很多时候会根据创建时间或者其他因素，列出一个 Collection 中前 100 个 Member，这时可以在 URI 参数中指明排序参数，例如/users?sort=age,desc。

- 搜索
  - 当一个资源的 Member 太多时，用户可能想通过搜索，快速找到所需要的 Member，或着想搜下有没有名字为 xxx 的某类资源，这时候就需要提供搜索功能。
  - 搜索建议按模糊匹配来搜索。

##### 域名

- API 的域名设置主要有两种方式：
  - `https://marmotedu.com/api`，这种方式适合 API 将来不会有进一步扩展的情况，比如刚开始 marmotedu.com 域名下只有一套 API 系统，未来也只有这一套 API 系统。
  - `https://iam.api.marmotedu.com`，如果 marmotedu.com 域名下未来会新增另一个系统 API，这时候最好的方式是每个系统的 API 拥有专有的 API 域名，
    比如：storage.api.marmotedu.com，network.api.marmotedu.com。
    腾讯云的域名就是采用这种方式。

#### 总结

- REST vs RESTful API
  - REST 是一种 API 规范
  - RESTful API 则是满足这种规范的 API 接口
  - RESTful API 的核心是规范

- REST 规范
  - 资源通过 URI 来标识，资源名使用名词而不是动词，并且用名词复数表示，资源都是分为 Collection 和 Member 两种。

- RESTful API 设计原则
  - 对资源的操作
    - RESTful API 中，分别使用 POST、DELETE、PUT、GET 来表示 REST 资源的增删改查。
    - HTTP 方法、Collection、Member 不同组合会产生不同的操作，具体的映射你可以看下「REST 资源操作映射为 HTTP 方法」部分的表格。
  - 统一的返回格式
    - 为了方便用户使用和理解，每个 RESTful API 的返回格式、错误和正确消息的返回格式，都应该保持一致。
  - 版本管理
    - RESTful API 需要支持 API 版本，并且版本应该能够向前兼容。
    - 建议将版本号放在 URL 中，例如 /v1/users，这种形式比较直观。
  - 命名风格
    - 脊柱命名法（小写 + 短线），比如：server-address。
  - 查询接口
    - 应该支持分页 / 过滤 / 排序 / 搜索功能，这些功能可以用同一套机制来实现。
  - 域名风格
    - 可以采用 `https://marmotedu.com/api` 和 `https://iam.api.marmotedu.com` 两种格式。

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

  [1]: https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm
  [2]: https://docs.github.com/en/rest
  [3]: https://cloud.google.com/apis/design

# 《程序员修炼攻略》分析笔记

## 第15章 微服务

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- 微服务架构
- 微服务和 SOA
- 设计模式和最佳实践
- 相关资源

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 微服务架构

- Martin Fowler 关于微服务架构的介绍
  - [Microservice Architecture][1]
  - [中文版][2]
  - [视频][3]

- 各家对微服务的理解
  - [AWS 的理解 - What are Microservices?][4]
  - [Microsoft 的理解 - Microservices architecture style][5]
  - [Pivotal 的理解 - Microservices。][6]

- [IBM 红皮书：Microservices Best Practices for Java][7]
  - 不仅通过把 Spring Boot 和 Dropwizard 来架建 Java 的微服务，
  - 而且还谈到了一些标准的架构模型，如服务注册、服务发现、API 网关、服务通讯、数据处理、应用安全、测试、部署、运维等，是相当不错的一本书

- [微服务设计][8]
  - 这本书全面介绍了微服务的建模、集成、测试、部署和监控，通过一个虚构的公司讲解了如何建立微服务架构。

- Nginx 上的一组微服务架构的系列文章
  - [Introduction to Microservices][9]
  - [Building Microservices: Using an API Gateway][10]
  - [Building Microservices: Inter-Process Communication in a Microservices Architecture][11]
  - [Service Discovery in a Microservices Architecture][12]
  - [Event-Driven Data Management for Microservices][13]
  - [Choosing a Microservices Deployment Strategy][14]
  - [Refactoring a Monolith into Microservices][15]

- [Auto0 Blog][56] 上一系列的微服务的介绍
  - [An Introduction to Microservices, Part 1][16]
  - [API Gateway. An Introduction to Microservices, Part 2][17]
  - [An Introduction to Microservices, Part 3: The Service Registry][18]
  - [Intro to Microservices, Part 4: Dependencies and Data Sharing][19]
  - [API Gateway: the Microservices Superglue][20]

- Dzone 的 Spring Boot 的教程
  - [Microservices With Spring Boot - Part 1 - Getting Started][21]
  - [Microservices With Spring Boot - Part 2 - Creating a Forex Microservice][22]
  - [Microservices With Spring Boot - Part 3 - Creating Currency Conversion Microservice][23]
  - [Microservices With Spring Boot - Part 4 - Using Ribbon for Load Balancing][24]
  - [Microservices With Spring Boot - Part 5 - Using Eureka Naming Server][25]

- 推荐一套时髦的架构
  - 前端：[React.js][26] 或 [Vue.js][27]。
  - 后端：[Go 语言][28] + 微服务工具集 [Go kit][29]，因为是微服务了，所以，每个服务的代码就简单了。既然简单了，也就可以用任何语言了，所以，我推荐 Go 语言。
  - 通讯：[gRPC][30]，这是 Google 远程调用的一个框架，它比 Restful 的调用要快 20 倍到 50 倍的样子。
  - API：[Swagger][31]，Swagger 是一种 Restful API 的简单但强大的表示方式，标准的，语言无关，这种表示方式不但人可读，而且机器可读。
    可以作为 Restful API 的交互式文档，也可以作为 Restful API 形式化的接口描述，生成客户端和服务端的代码。
    今天，所有的 API 应该都通过 Swagger 来完成。
  - 网关：[Envoy][32] 其包含了服务发现、负载均衡和熔断等这些特性，也是一个很有潜力的网关。
    当然，Kubernetes 也是很好的，而且它也是高扩展的，所以，完全可以把 Envoy 通过 Ingress 集成进 Kubernetes。
    这里有一个开源项目就是干这个事的 - [contour][33]。
  - 日志监控：[fluentd][34] + [ELK][35]。
  - 指标监控：[Prometheus][36]。
  - 调用跟踪：[Jaeger][37] 或是 [Zipkin][38]，当然，后者比较传统一些，前者比较时髦，最重要的是，其可以和 Prometheus 和 Envory 集成。
  - 自动化运维：[Docker][39] + [Kubernetes][40]。

#### 微服务和 SOA

- [《Microservices vs. Service-Oriented Architecture》][41]
  - 通过这本书，你可以学到服务化架构的一些事实，还有基础的 SOA 和微服务的架构知识，以及两种架构的不同。

- 对比 SOA 和 微服务
  - [DZone: Microservices vs. SOA][42]
  - [DZone: Microservices vs. SOA - Is There Any Difference at All?][43]
  - [Microservices, SOA, and APIs: Friends or enemies?][44]

- 对比微服务和其他架构
  - [PaaS vs. IaaS for Microservices Architectures: Top 6 Differences][45]
  - [Microservices vs. Monolithic Architectures: Pros, Cons, and How Cloud Foundry (PaaS) Can Help][46]
  - [Microservices - Not A Free Lunch!][47]
  - [The Hidden Costs Of Microservices][48]

#### 设计模式和最佳实践

- [Microservice Patterns][49]
  - 微服务架构的设计模式和最佳实践。

- [Microservice Antipatterns and Pitfalls][50]
  - 微服务架构的一些已知的反模式和陷阱。

- [Microservice Architecture: All The Best Practices You Need To Know][51]
  - 这是一篇长文，里面讲述了什么是微服务、微服务架构的优缺点、微服务最大的挑战和解决方案是什么、如何避免出错，以及构建微服务架构的最佳实践等多方面的内容。

- [Best Practices for Building a Microservice Architecture ][52]
  - 这篇文章分享了构建微服务架构的最佳实践。

- [Simplicity by Distributing Complexity][53]
  - 这是一篇讲如何使用事件驱动构建微服务架构的文章，其中有很多不错的设计上的基本原则。

#### 相关资源

- [Microservices Resource Guide][54]
  - 这个网页上是 Martin Fowler 为我们挑选的和微服务相关的文章、视频、书或是 podcast。

- [Awesome Microservices][55]
  - 一个各种微服务资源和相关项目的集中地。

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

  [1]: https://martinfowler.com/articles/microservices.html
  [2]: https://blog.csdn.net/wurenhai/article/details/37659335
  [3]: https://www.youtube.com/watch?v=wgdBVIX9ifAo
  [4]: https://aws.amazon.com/microservices/
  [5]: https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices
  [6]: https://tanzu.vmware.com/microservices
  [7]: https://www.redbooks.ibm.com/redbooks/pdfs/sg248357.pdf
  [8]: https://book.douban.com/subject/26772677/
  [9]: https://www.nginx.com/blog/introduction-to-microservices/
  [10]: https://www.nginx.com/blog/building-microservices-using-an-api-gateway/
  [11]: https://www.nginx.com/blog/building-microservices-inter-process-communication/
  [12]: https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/
  [13]: https://www.nginx.com/blog/event-driven-data-management-microservices/
  [14]: https://www.nginx.com/blog/deploying-microservices/
  [15]: https://www.nginx.com/blog/refactoring-a-monolith-into-microservices/
  [16]: https://auth0.com/blog/an-introduction-to-microservices-part-1/
  [17]: https://auth0.com/blog/an-introduction-to-microservices-part-2-API-gateway/
  [18]: https://auth0.com/blog/an-introduction-to-microservices-part-3-the-service-registry/
  [19]: https://auth0.com/blog/introduction-to-microservices-part-4-dependencies/
  [20]: https://auth0.com/blog/apigateway-microservices-superglue/
  [21]: https://dzone.com/articles/microservices-with-spring-boot-part-1-getting-star
  [22]: https://dzone.com/articles/microservices-with-spring-boot-part-2-creating-a-f
  [23]: https://dzone.com/articles/microservices-with-spring-boot-part-3-creating-cur
  [24]: https://dzone.com/articles/microservices-with-spring-boot-part-4-using-ribbon
  [25]: https://dzone.com/articles/microservices-with-spring-boot-part-5-using-eureka
  [26]: https://reactjs.org/
  [27]: https://vuejs.org/
  [28]: https://go.dev/
  [29]: https://gokit.io/
  [30]: https://grpc.io/
  [31]: https://swagger.io/
  [32]: https://www.envoyproxy.io/
  [33]: https://github.com/projectcontour/contour
  [34]: https://www.fluentd.org/
  [35]: https://www.elastic.co/webinars/introduction-elk-stack
  [36]: https://prometheus.io/
  [37]: https://www.jaegertracing.io/docs/1.38/
  [38]: https://zipkin.io/
  [39]: https://www.docker.com/
  [40]: https://kubernetes.io/
  [41]: https://www.nginx.com/resources/library/microservices-vs-soa/
  [42]: https://dzone.com/articles/microservices-vs-soa-2
  [43]: https://dzone.com/articles/microservices-vs-soa-is-there-any-difference-at-al
  [44]: https://developer.ibm.com/depmodels/cloud/
  [45]: http://blog.altoros.com/microservices-architectures-paas-vs-iaas-top-6-differences.html
  [46]: https://www.slideshare.net/altoros/microservices-vs-monolithic-architectures-pros-and-cons
  [47]: http://highscalability.com/blog/2014/4/8/microservices-not-a-free-lunch.html
  [48]: https://www.stackbuilders.com/blog/the-hidden-costs-of-microservices/
  [49]: https://microservices.io/
  [50]: https://www.oreilly.com/content/microservices-antipatterns-and-pitfalls/
  [51]: https://codingsans.com/blog/microservice-architecture-best-practices
  [52]: https://www.vinaysahni.com/best-practices-for-building-a-microservice-architecture
  [53]: https://engineering.zalando.com/posts/2018/01/simplicity-by-distributing-complexity.html
  [54]: https://martinfowler.com/microservices/
  [55]: https://github.com/mfornos/awesome-microservices/
  [56]: https://auth0.com/blog/

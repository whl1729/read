# 《程序员修炼攻略》分析笔记

## 第16章 容器化和自动化运维

### Q1：这一章的内容属于哪一类别？

计算机/方法论。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- Docker
- Kubernetes
- Docker 和 Kubernetes 资源汇总

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### Docker

- 初步体验
  - 你可以先看一下 Docker 的官方介绍 [Docker Overview][1]。
  - 然后再去一个 Web 在线的 Playground 上体验一下：[Katacoda Docker Playground][2] 或者是 [Play With Docker][3]。（伍注：前者被关闭了。）
  - 接着跟着 [Learn Docker][4] 这个文档中的教程自己安装一个 Docker 的环境，实操一把。
  - 然后跟着 [Docker Curriculum][5] 这个超详细的教程玩一下 Docker。

- 阅读 Docker 官方文档：[Docker Documentation][6]。
  - 这是学习 Docker 的最好方式。

- 关于 Docker 底层技术细节，可以参考以下酷壳博客：
  - [Docker 基础技术：Linux Namespace（上）][7]
  - [Docker 基础技术：Linux Namespace（下）][8]
  - [Docker 基础技术：Cgroup][9]
  - [Docker 基础技术：AUFS][10]
  - [Docker 基础技术：DeviceMapper][11]

- Docker 网络相关的文章
  - [A container networking overview][12]
  - [Docker networking 101 - User defined networks][13]
  - [Understanding CNI (Container Networking Interface)][14]
  - [Using CNI with Docker][15]

- Docker 网络解决方案
  - [Calico][16]
  - [Flannel][17]
  - [Weave][18]

- Docker 网络问题诊断工具
  - [netshoot][19]

- Docker 网络解决方案的性能对比
  - [Battlefield: Calico, Flannel, Weave and Docker Overlay Network][20]
  - [Comparison of Networking Solutions for Kubernetes][21]
  - [Docker Overlay Networks: Performance analysis in high-latency enviroments][22]

- Docker 性能相关的文章
  - [IBM Research Report: An Updated Performance Comparison of Virtual Machines and Linux Containers][23]
  - [An Introduction to Docker and Analysis of its Performance][24]

- Docker 存储相关的文章
  - [Storage Concepts in Docker: Network and Cloud Storage][25]
  - [Storage Concepts in Docker: Persistent Storage][26]
  - [Storage Concepts in Docker: Shared Storage and the VOLUME directive][27]

- Docker 运维相关的文章
  - [Docker Monitoring with the ELK Stack: A Step-by-Step Guide][28]

- Docker 系列文章
  - [Valuable Docker Links][29]

- Docker 最佳实践
  - [Best Practices for Dockerfile][30]
    - Docker 官方文档里的 Dockerfile 的最佳实践。
  - [Docker Best Practices][31]
    - 这里收集汇总了存在于各个地方的使用 Docker 的建议和实践。
  - [Container Best Practices][32]
    - 来自 Atomic 项目，是一个介绍容器化应用程序的架构、创建和管理的协作型文档项目。
  - [Eight Docker Development Patterns][33]（[中文版][34]）
    - 八个 Docker 的开发模式：共享基础容器、共享同一个卷的多个开发容器、开发工具专用容器、测试环境容器、编译构建容器、防手误的安装容器、默认服务容器、胶黏容器。

#### Kubernetes

- Kubernetes 前世今生的一篇论文
  - [Borg, Omega, and Kubernetes][35]
    - 看看 Google 这十几年来从这三个容器管理系统中得到的经验教训。

- Kubernetes 电子书
  - [《Kubernetes in Action》][36]
    - 感觉写的非常好，一本很完美的教科书，抽丝剥茧，图文并茂。
    - 如果你只想读一本有关 Kubernetes 的书来学习 Kubernetes，那么我推荐你就选这本。
  - [《Kubernetes Handbook][37]
    - 这本书记录了作者从零开始学习和使用 Kubernetes 的心路历程，着重于经验分享和总结，同时也会有相关的概念解析。
    - 希望能够帮助你少踩坑，少走弯路，还会指引你关注 kubernetes 生态周边，如微服务构建、DevOps、大数据应用、Service Mesh、Cloud Native 等领域。
  - [《Kubernetes 指南][38]
    - 这本书旨在整理平时在开发和使用 Kubernetes 时的参考指南和实践总结，形成一个系统化的参考指南以方便查阅。

- Kubernetes 的官方网站：[Kubernetes.io][39]
  - 上面不但有 [全面的文档][40]，也包括一个很不错的 [官方教程][41]。

- 一些交互式教程
  - [Katacoda][42] （已经关闭）
  - [Kubernetes Bootcamp][43]

- 一些文章
  - [Kubernetes tips & tricks][44]
  - [Achieving CI/CD with Kubernetes][45]
  - [How to Set Up Scalable Jenkins on Top of a Kubernetes Cluster][46]
  - 10 Most Common Reasons Kubernetes Deployments Fail （[Part I][47] 和 [Part II][48]）
  - [How to Monitor Kubernetes][49]
  - [Logging in Kubernetes with Fluentd and Elasticsearch][50]
  - [Kubernetes Monitoring: Best Practices, Methods, and Existing Solutions][51]

- 网络相关文章
  - [Kubernetes 101 - Networking][52]
  - [Kubernetes networking 101 - Pods][53]
  - [Kubernetes networking 101 - Services][54]
  - [Kubernetes networking 101 - (Basic) External access into the cluster][55]
  - [Kubernetes Networking 101 - Ingress resources][56]
  - [Getting started with Calico on Kubernetes][57]

- CI/CD 相关文章
  - [Automated Image Builds with Jenkins, Packer, and Kubernetes][58]
  - [Jenkins setups for Kubernetes and Docker Workflow][59]
  - [Lab: Build a Continuous Deployment Pipeline with Jenkins and Kubernetes][60]

- 最佳实践
  - [Kubernetes Best Practices (by Sachin Arote)][61]
    - AWS 工程师总结的最佳实践。
  - [Kubernetes Best Practices (by Sandeep Dinesh)][62]
    - Google 云平台工程师总结的最佳实践。

#### Docker 和 Kubernetes 资源汇总

- [Awesome Docker][63]

- [Awesome Kubernetes][64]

- [The New Stack eBook Series][65]：非常完整和详实的 Docker 和 Kubernetes 生态圈的所有东西。
  - [Book 01: The Docker Container Ecosystem][66]
  - [Book 02: Applications & Microservices with Docker & Containers][67]
  - [Book 03: Automation & Orchestration with Docker & Containers][68]
  - [Book 04: Network, Security & Storage with Docker & Containers][69]
  - [Book 05: Monitoring & Management with Docker & Containers][70]
  - [Book 06: Use Cases for Kubernetes][71]
  - [Book 07: State of the Kubernetes Ecosystem][72]
  - [Book 08: Kubernetes Deployment & Security Patterns][73]
  - [Book 09: CI/CD with Kubernetes][74]
  - [Book 10: Kubernetes solutions Directory][75]
  - [Book 11: Guid to Cloud-Native Microservices][76]

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

  [1]: https://docs.docker.com/get-started/overview/
  [2]: https://www.katacoda.com/courses/docker/playground
  [3]: https://training.play-with-docker.com/
  [4]: https://github.com/dwyl/learn-docker
  [5]: https://docker-curriculum.com/
  [6]: https://docs.docker.com/
  [7]: https://coolshell.cn/articles/17010.html
  [8]: https://coolshell.cn/articles/17029.html
  [9]: https://coolshell.cn/articles/17049.html
  [10]: https://coolshell.cn/articles/17061.html
  [11]: https://coolshell.cn/articles/17200.html
  [12]: https://jvns.ca/blog/2016/12/22/container-networking/
  [13]: http://www.dasblinkenlichten.com/docker-networking-101-user-defined-networks/
  [14]: http://www.dasblinkenlichten.com/understanding-cni-container-networking-interface/
  [15]: http://www.dasblinkenlichten.com/using-cni-docker/
  [16]: https://github.com/projectcalico/calico
  [17]: https://github.com/flannel-io/flannel
  [18]: https://github.com/weaveworks/weave
  [19]: https://github.com/nicolaka/netshoot
  [20]: https://www.ijuned.com/battlefield-calico-flannel-weave-and-docker-overlay-network-arthur-chunqi-lis-blog/
  [21]: https://dominoweb.draco.res.ibm.com/reports/rc25482.pdf
  [22]: http://paper.ijcsns.org/07_book/201703/20170327.pdf
  [23]: http://cloud-mechanic.blogspot.com/2014/10/storage-concepts-in-docker-network-and.html
  [24]: http://cloud-mechanic.blogspot.com/2014/10/storage-concepts-in-docker-persistent.html
  [25]: http://cloud-mechanic.blogspot.com/2014/10/storage-concepts-in-docker.html
  [26]: https://logz.io/learn/docker-monitoring-elk-stack/
  [27]: https://nkode.io/
  [28]: https://logz.io/learn/docker-monitoring-elk-stack/
  [29]: https://kratzke.mylab.th-luebeck.de/blog/2014/08/24/valuable-docker-links/
  [30]: https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
  [31]: https://github.com/FuriKuri/docker-best-practices
  [32]: http://docs.projectatomic.io/container-best-practices/
  [33]: http://hokstad.com/docker/patterns
  [34]: https://www.infoq.cn/article/2014/10/seven-docker-develop-pattern
  [35]: https://static.googleusercontent.com/media/research.google.com/zh-CN//pubs/archive/44843.pdf
  [36]: https://www.oreilly.com/library/view/kubernetes-in-action/9781617293726/
  [37]: https://jimmysong.io/kubernetes-handbook/
  [38]: https://kubernetes.feisky.xyz/
  [39]: https://kubernetes.io/
  [40]: https://kubernetes.io/docs/home/
  [41]: https://kubernetes.io/docs/tutorials/kubernetes-basics/
  [42]: https://www.katacoda.com/
  [43]: https://kubernetesbootcamp.github.io/kubernetes-bootcamp/
  [44]: https://opsnotice.xyz/kubernetes-tips-tricks/
  [45]: http://theremotelab.com/blog/achieving-ci-cd-with-k8s/
  [46]: https://dzone.com/articles/how-to-setup-scalable-jenkins-on-top-of-a-kubernet
  [47]: https://kukulinski.com/10-most-common-reasons-kubernetes-deployments-fail-part-1/
  [48]: https://kukulinski.com/10-most-common-reasons-kubernetes-deployments-fail-part-2/
  [49]: https://sysdig.com/blog/monitoring-kubernetes/
  [50]: http://www.dasblinkenlichten.com/logging-in-kubernetes-with-fluentd-and-elasticsearch/
  [51]: https://dzone.com/articles/kubernetes-monitoring-best-practices-methods-and-e
  [52]: http://www.dasblinkenlichten.com/kubernetes-101-networking/
  [53]: http://www.dasblinkenlichten.com/kubernetes-networking-101-pods/
  [54]: http://www.dasblinkenlichten.com/kubernetes-networking-101-services/
  [55]: http://www.dasblinkenlichten.com/kubernetes-networking-101-basic-external-access-into-the-cluster/
  [56]: http://www.dasblinkenlichten.com/kubernetes-networking-101-ingress-resources/
  [57]: http://www.dasblinkenlichten.com/getting-started-with-calico-on-kubernetes/
  [58]: https://cloud.google.com/architecture/automated-build-images-with-jenkins-kubernetes#kubernetes_architecture
  [59]: http://iocanel.com/2015/09/jenkins-setups-for-kubernetes-and-docker-workflow/
  [60]: https://github.com/GoogleCloudPlatform/continuous-deployment-on-kubernetes
  [61]: https://sachin34268.medium.com/kubernetes-best-practices-9b1435a4cb53
  [62]: https://speakerdeck.com/thesandlord/kubernetes-best-practices
  [63]: https://github.com/veggiemonk/awesome-docker
  [64]: https://github.com/ramitsurana/awesome-kubernetes
  [65]: https://thenewstack.io/new-ebook-the-new-stacks-quick-guide-to-cloud-native-storage/
  [66]: https://thenewstack.io/ebooks/docker-and-containers/the-docker-container-ecosystem/
  [67]: https://thenewstack.io/ebooks/docker-and-containers/applications-microservices-docker-containers/
  [68]: https://thenewstack.io/ebooks/docker-and-containers/automation-orchestration-docker-containers/
  [69]: https://thenewstack.io/ebooks/docker-and-containers/networking-security-storage-docker-containers/
  [70]: https://thenewstack.io/ebooks/docker-and-containers/monitoring-management-docker-containers/
  [71]: https://thenewstack.io/ebooks/use-cases/use-cases-for-kubernetes/
  [72]: https://thenewstack.io/ebooks/kubernetes/state-of-kubernetes-ecosystem-second-edition-2020
  [73]: https://thenewstack.io/ebooks/kubernetes/kubernetes-deployment-and-security-patterns/
  [74]: https://thenewstack.io/ebooks/kubernetes/ci-cd-with-kubernetes/
  [75]: https://thenewstack.io/ebooks/kubernetes/kubernetes-solutions-directory/
  [76]: https://thenewstack.io/ebooks/microservices/cloud-native-microservices-2018/

# 《程序员练级攻略》分析笔记

## 第11章 数据库

### Q1：这一章的内容属于哪一类别

计算机/方法论。

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- 关系型数据库
- NoSQL 数据库
- 各种 NoSQL 数据库
  - 列数据库 Column Database
  - 文档数据库 Document Database - MongoDB, SimpleDB, CouchDB
  - 数据结构数据库 Data structure Database - Redis
  - 时序数据库 Time-Series Database
  - 图数据库 - Graph Platform
  - 搜索数据库 - ElasticSearch

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

- 对于数据库方向，重点就是两种数据库
  - 一种是以 SQL 为代表的关系型数据库
  - 另一种是以非 SQL 为代表的 NoSQL 数据库。

- 关系型数据库主要有三个：Oracle、MySQL 和 Postgres。

- NoSQL 主要是解决了关系型数据库中的各种问题。
  - 第一个大问题就是数据的 Schema 非常多，用关系型数据库来表示不同的 Data Schema 是非常笨拙的，所以要有不同的数据库（如时序型、键值对型、搜索型、文档型、图结构型等）。
  - 另一个大问题是，关系型数据库的 ACID 是一件很讨厌的事，这极大地影响了数据库的性能和扩展性，所以 NoSQL 在这上面做了相应的妥协以解决大规模伸缩的问题。

#### 关系型数据库

- Oracle
  - [《Oracle Database 9i/10g/11g 编程艺术》][1]

- [MySQL 官方手册][2]

- MySQL 官方 PPT （也要学习一下）
  - [How to Analyze and Tune MySQL Queries for Better Performance][3]
  - [MySQL Performance Tuning 101][4]
  - [MySQL Performance Schema & Sys Schema][5]
  - [MySQL Performance: Demystified Tuning & Best Practices][6]
  - [MySQL Security Best Practices][7]
  - [MySQL Cluster Deployment Best Practices][8]
  - [MySQL High Availability with InnoDB Cluster][9]

- [《高性能 MySQL》][10]

- MySQL 的内部原理
  - [《MySQL 技术内幕：InnoDB 存储引擎》][11]
  - [MySQL Internals Manual][12]：官方文档

- [《数据库的索引设计与优化》][13]
  - 数据库的索引设计和优化也是非常关键的。
  - 在系统架构上，在分布式架构中，索引技术也是非常重要的。

- MySQL 的一些文章
  - [MySQL 索引背后的数据结构及算法原理][14]
  - [Some study on database storage internals][15]
  - [Sharding Pinterest: How we scaled our MySQL fleet][16]
  - [Guide to MySQL High Availability][17]
  - [Choosing MySQL High Availability Solutions][18]
  - [High availability with MariaDB TX: The definitive guide][19]

- MySQL 资源列表：[Awesome MySQL][20]

- MySQL 的分支
  - MySQL 有两个比较有名的分支，一个是 Percona，另一个是 MariaDB。
  - 它们官网上的 Resources 页面中有很多不错的资源和文档，可以经常看看：[Percona Resources][21]、[MariaDB Resources][22]
  - 它们的开发博客中也有很多不错的文章，分别为 [Percona Blog][23] 和 [MariaDB Blog][24]。

- MySQL 的一些经验型文章
  - [Booking.com: Evolution of MySQL System Design][25]: Booking.com 的 MySQL 数据库使用的演化，其中有很多不错的经验分享，我相信也是很多公司会遇到的的问题。
  - [Tracking the Money - Scaling Financial Reporting at Airbnb][26]: Airbnb 的数据库扩展的经验分享。
  - [Why Uber Engineering Switched from Postgres to MySQL][27]: 这里无意比较两个数据库，主要是想让你从中学习到一些经验和技术细节。

- MySQL 的集群复制
  - [Monitoring Delayed Replication, With A Focus On MySQL][28]
  - [Mitigating replication lag and reducing read load with freno][29]
  - [Better Parallel Replication for MySQL][30]
  - [Evaluating MySQL Parallel Replication Part 2: Slave Group Commit][31]
  - [Evaluating MySQL Parallel Replication Part 3: Benchmarks in Production][32]
  - [Evaluating MySQL Parallel Replication Part 4: More Benchmarks in Production][33]
  - [Evaluating MySQL Parallel Replication Part 4, Annex: Under the Hood][34]

- MySQL 的数据分区
  - [StackOverflow: MySQL sharding approaches?][35]
  - [Why you don’t want to shard][36]
  - [How to Scale Big Data Applications][37]
  - [MySQL Sharding with ProxySQL][38]

- 各个公司做 MySQL Sharding 的一些经验分享
  - [MailChimp: Using Shards to Accommodate Millions of Users][39]
  - [Uber: Code Migration in Production: Rewriting the Sharding Layer of Uber’s Schemaless Datastore][40]
  - [Sharding & IDs at Instagram][41]
  - [Airbnb: How We Partitioned Airbnb’s Main Database in Two Weeks][42]

#### NoSQL 数据库

- Martin Fowler
  - 在 YouTube 上分享的 NoSQL 介绍：[Introduction To NoSQL][43]
  - 参与编写的一本小书： [NoSQL Distilled - NoSQL 精粹][44]

- [NoSQL Databases: a Survey and Decision Guidance][45]
  - 这篇文章可以带你自上而下地从 CAP 原理到开始了解 NoSQL 的种种技术。

- [Distribution, Data, Deployment: Software Architecture Convergence in Big Data System][46]
  - 这是卡内基·梅隆大学的一篇讲分布式大数据系统的论文。
  - 其中主要讨论了在大数据时代下的软件工程中的一些关键点，也说到了 NoSQL 数据库。

- [No Relation: The Mixed Blessings of Non-Relational Database][47]
  - 这篇论文是 HBase 的基础，虽然年代有点久远，但可以帮你了解到，对各种非关系型数据存储优缺点的一个很好的比较。

- [NoSQL Data Modeling Techniques][48]
  - NoSQL 建模技术。这篇文章我曾经翻译在了 CoolShell 上，标题为 [NoSQL 数据建模技术][49]，供你参考。

- [MongoDB - Data Modeling Introduction][50]
  - 虽然这是 MongoDB 的数据建模介绍，但是其很多观点可以用于其它的 NoSQL 数据库。

- [Firebase - Structure Your Database][51]
  - Google 的 Firebase 数据库使用 JSON 建模的一些最佳实践。

- [Visual Guide to NoSQL Systems。][52]
  - 因为 CAP 原理，所以当你需要选择一个 NoSQL 数据库的时候，你应该看看这篇文档。

- 选 SQL 还是 NoSQL
  - [SQL vs. NoSQL Databases: What’s the Difference?][53]
  - [Salesforce: SQL or NoSQL][54]

#### 各种 NoSQL 数据库

##### 列数据库 Column Database

- Cassandra
  - 沃尔玛实验室有两篇文章值得一读
    - [Avoid Pitfalls in Scaling Cassandra Cluster at Walmart][55]
    - [Storing Images in Cassandra at Walmart][56]
  - [Yelp: How We Scaled Our Ad Analytics with Apache Cassandra][57]: Yelp 的这篇博客也有一些相关的经验和教训。
  - [Discord: How Discord Stores Billions of Messages][58]: Discord 公司分享的一个如何存储十亿级消息的技术文章。
  - [Cassandra at Instagram][59]: Instagram 的一个 PPT，其中介绍了 Instagram 中是怎么使用 Cassandra 的。
  - [Netflix: Benchmarking Cassandra Scalability on AWS - Over a million writes per second][60]: Netflix 公司在 AWS 上给 Cassandra 做的一个 Benchmark。

- HBase
  - [Imgur Notification: From MySQL to HBASE][61]
  - [Pinterest: Improving HBase Backup Efficiency][62]
  - [IBM : Tuning HBase performance][63]
  - [HBase File Locality in HDFS][64]
  - [Apache Hadoop Goes Realtime at Facebook][65]
  - [Storage Infrastructure Behind Facebook Messages: Using HBase at Scale][66]
  - [GitHub: Awesome HBase][67]
  - [《HBase 实战》][68]：偏实践
  - [《HBase 权威指南》][69]：大而全、手册型
  - [The Apache HBase™ Reference Guide][70]: 官方文档

- 另外两个列数据库：
  - [ClickHouse - Open Source Distributed Column Database at Yandex][71]
  - [Scaling Redshift without Scaling Costs at GIPHY][72]

##### 文档数据库 Document Database - MongoDB, SimpleDB, CouchDB

- [Data Points - What the Heck Are Document Databases?][73]
- [eBay: Building Mission-Critical Multi-Data Center Applications with MongoDB][74]
- [The AWS and MongoDB Infrastructure of Parse: Lessons Learned][75]
- [Migrating Mountains of Mongo Data][76]
- [Couchbase Ecosystem at LinkedIn][77]
- [SimpleDB at Zendesk][78]
- [Github: Awesome MongoDB][79]

##### 数据结构数据库 Data structure Database - Redis

- [Learn Redis the hard way (in production) at Trivago][80]
- [Twitter: How Twitter Uses Redis To Scale - 105TB RAM, 39MM QPS, 10,000+ Instances][81]
- [Slack: Scaling Slack’s Job Queue - Robustly Handling Billions of Tasks in Milliseconds Using Kafka and Redis][82]
- [GitHub: Moving persistent data out of Redis at GitHub][83]
- [Instagram: Storing Hundreds of Millions of Simple Key-Value Pairs in Redis][84]
- [Redis in Chat Architecture of Twitch (from 27:22)][85]
- [Deliveroo: Optimizing Session Key Storage in Redis][86]
- [Deliveroo: Optimizing Redis Storage][87]
- [GitHub: Awesome Redis][88]

##### 时序数据库 Time-Series Database

- [What is Time-Series Data & Why We Need a Time-Series Database][89]
- [Time Series Data: Why and How to Use a Relational Database instead of NoSQL][90]
- [Beringei: High-performance Time Series Storage Engine @Facebook][91]
- [Introducing Atlas: Netflix’s Primary Telemetry Platform @Netflix][92]
- [Building a Scalable Time Series Database on PostgreSQL][93]
- [Scaling Time Series Data Storage - Part I @Netflix][94]
- [Design of a Cost Efficient Time Series Store for Big Data][95]
- [GitHub: Awesome Time-Series Database][96]

##### 图数据库 - Graph Platform

- [《Graph Database》][99]：一本免费的电子书。

- 一些图数据库的介绍文章
  - [Handling Billions of Edges in a Graph Database][100]
  - [Neo4j case studies with Walmart, eBay, AirBnB, NASA, etc][101]
  - [FlockDB: Distributed Graph Database for Storing Adjacency Lists at Twitter][102]
  - [JanusGraph: Scalable Graph Database backed by Google, IBM and Hortonworks][103]
  - [Amazon Neptune][104]

##### 搜索数据库 - ElasticSearch

- [Elasticsearch: The Definitive Guide][105]
  - 这是官网方的 ElasticSearch 的学习资料，基本上来说，看这个就够了。

- 4 篇和性能调优相关的工程实践
  - [Elasticsearch Performance Tuning Practice at eBay][106]
  - [Elasticsearch at Kickstarter][107]
  - [9 tips on ElasticSearch configuration for high performance][108]
  - [Elasticsearch In Production - Deployment Best Practices][109]

- GitHub 上的资源列表
  - [GitHub: Awesome ElasticSearch][110]

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

  [1]: https://book.douban.com/subject/5402711/
  [2]: https://dev.mysql.com/doc/
  [3]: https://www.slideshare.net/oysteing/how-to-analyze-and-tune-sql-queries-for-better-performance-percona15
  [4]: https://www.slideshare.net/MirkoOrtensi/mysql-performance-tuning-101
  [5]: https://dev.mysql.com/doc/refman/8.0/en/performance-schema.html
  [6]: http://dimitrik.free.fr/Presentations/MySQL_Perf-Tuning-OOW_2014-dim-keynote.key.pdf
  [7]: https://www.computer.org/publications/tech-news/trends/mysql-security-best-practices
  [8]: https://pdfslide.net/documents/mysql-cluster-deployment-best-practices-presentation.html
  [9]: https://www.slideshare.net/mattalord/mysql-high-availability-innodb-clusters
  [10]: https://book.douban.com/subject/23008813/
  [11]: https://book.douban.com/subject/24708143/
  [12]: https://dev.mysql.com/doc/internals/en/
  [13]: https://book.douban.com/subject/26419771/
  [14]: http://blog.codinglabs.org/articles/theory-of-mysql-index.html
  [15]: https://kousiknath.medium.com/data-structures-database-storage-internals-1f5ed3619d43
  [16]: https://medium.com/pinterest-engineering/sharding-pinterest-how-we-scaled-our-mysql-fleet-3f341e96ca6f
  [17]: https://www.mysql.com/cn/why-mysql/white-papers/mysql-guide-to-high-availability-solutions/
  [18]: https://dzone.com/articles/choosing-mysql-high-availability-solutions
  [19]: https://mariadb.com/wp-content/uploads/2019/04/mariadb-platform-high-availability-guide_whitepaper_1001.pdf
  [20]: https://shlomi-noach.github.io/awesome-mysql/
  [21]: https://www.percona.com/resources
  [22]: https://mariadb.com/resources/
  [23]: https://www.percona.com/blog/
  [24]: https://mariadb.com/resources/blog/
  [25]: https://www.percona.com/live/mysql-conference-2015
  [26]: https://medium.com/airbnb-engineering/tracking-the-money-scaling-financial-reporting-at-airbnb-6d742b80f040
  [27]: https://www.uber.com/en-JP/blog/postgres-to-mysql-migration/
  [28]: https://engineering.imvu.com/2013/01/09/monitoring-delayed-replication-with-a-focus-on-mysql/
  [29]: https://github.blog/2017-10-13-mitigating-replication-lag-and-reducing-read-load-with-freno/
  [30]: https://medium.com/booking-com-infrastructure/better-parallel-replication-for-mysql-14e2d7857813
  [31]: https://medium.com/booking-com-infrastructure/evaluating-mysql-parallel-replication-part-2-slave-group-commit-459026a141d2
  [32]: https://medium.com/booking-com-infrastructure/evaluating-mysql-parallel-replication-part-3-benchmarks-in-production-db5811058d74
  [33]: https://medium.com/booking-com-infrastructure/evaluating-mysql-parallel-replication-part-4-more-benchmarks-in-production-49ee255043ab
  [34]: https://medium.com/booking-com-infrastructure/evaluating-mysql-parallel-replication-part-4-annex-under-the-hood-eb456cf8b2fb
  [35]: https://stackoverflow.com/questions/5541421/mysql-sharding-approaches
  [36]: https://www.percona.com/blog/2009/08/06/why-you-dont-want-to-shard/
  [37]: https://www.percona.com/sites/default/files/presentations/How%20to%20Scale%20Big%20Data%20Applications.pdf
  [38]: https://www.percona.com/blog/2016/08/30/mysql-sharding-with-proxysql/
  [39]: https://mailchimp.com/developer/
  [40]: https://www.uber.com/en-JP/blog/schemaless-rewrite/
  [41]: https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c
  [42]: https://medium.com/airbnb-engineering/how-we-partitioned-airbnb-s-main-database-in-two-weeks-55f7e006ff21
  [43]: https://www.youtube.com/watch?v=qI_g07C_Q5I
  [44]: https://book.douban.com/subject/25662138/
  [45]: https://medium.baqend.com/nosql-databases-a-survey-and-decision-guidance-ea7823a822d#.nhzop4d23
  [46]: https://ieeexplore.ieee.org/document/6774768
  [47]: http://ianvarley.com/UT/MR/Varley_MastersReport_Full_2009-08-07.pdf
  [48]: https://highlyscalable.wordpress.com/2012/03/01/nosql-data-modeling-techniques/
  [49]: https://coolshell.cn/articles/7270.html
  [50]: https://www.mongodb.com/docs/manual/core/data-modeling-introduction/
  [51]: https://firebase.google.com/docs/database/android/structure-data
  [52]: https://blog.nahurst.com/visual-guide-to-nosql-systems
  [53]: https://www.upwork.com/hiring/data/sql-vs-nosql-databases-whats-the-difference/
  [54]: https://engineering.salesforce.com/sql-or-nosql-9eaf1d92545b/
  [55]: https://medium.com/walmartglobaltech/avoid-pitfalls-in-scaling-your-cassandra-cluster-lessons-and-remedies-a71ca01f8c04
  [56]: https://medium.com/walmartglobaltech/building-object-store-storing-images-in-cassandra-walmart-scale-a6b9c02af593
  [57]: https://engineeringblog.yelp.com/2016/08/how-we-scaled-our-ad-analytics-with-cassandra.html
  [58]: https://discord.com/blog/how-discord-stores-billions-of-messages
  [59]: https://www.slideshare.net/DataStax/cassandra-at-instagram-2016
  [60]: https://netflixtechblog.com/benchmarking-cassandra-scalability-on-aws-over-a-million-writes-per-second-39f45f066c9e
  [61]: https://medium.com/imgur-engineering/imgur-notifications-from-mysql-to-hbase-9dba6fc44183
  [62]: https://medium.com/pinterest-engineering/improving-hbase-backup-efficiency-at-pinterest-86159da4b954
  [63]: https://www.ibm.com/docs/en/db2-big-sql/7.0?topic=locations-tuning-hbase-performance
  [64]: http://www.larsgeorge.com/2010/05/hbase-file-locality-in-hdfs.html
  [65]: http://borthakur.com/ftp/RealtimeHadoopSigmod2011.pdf
  [66]: https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.294.8459&rep=rep1&type=pdf
  [67]: https://github.com/rayokota/awesome-hbase
  [68]: https://book.douban.com/subject/25706541/
  [69]: https://book.douban.com/subject/10748460/
  [70]: https://hbase.apache.org/book.html#book
  [71]: https://clickhouse.com/
  [72]: https://engineering.giphy.com/scaling-redshift-without-scaling-costs/
  [73]: https://learn.microsoft.com/en-us/archive/msdn-magazine/2011/november/data-points-what-the-heck-are-document-databases
  [74]: https://www.mongodb.com/blog/post/ebay-building-mission-critical-multi-data-center-applications-with-mongodb
  [75]: https://medium.baqend.com/parse-is-gone-a-few-secrets-about-their-infrastructure-91b3ab2fcf71
  [76]: https://medium.com/build-addepar/migrating-mountains-of-mongo-data-63e530539952
  [77]: https://engineering.linkedin.com/blog/2017/12/couchbase-ecosystem-at-linkedin
  [78]: https://zendesk.engineering/resurrecting-amazon-simpledb-9404034ec506
  [79]: https://github.com/ramnes/awesome-mongodb
  [80]: https://tech.trivago.com/post/learn-redis-the-hard-way/
  [81]: http://highscalability.com/blog/2014/9/8/how-twitter-uses-redis-to-scale-105tb-ram-39mm-qps-10000-ins.html
  [82]: https://slack.engineering/scaling-slacks-job-queue/
  [83]: https://github.blog/2017-01-10-moving-persistent-data-out-of-redis/
  [84]: https://instagram-engineering.com/storing-hundreds-of-millions-of-simple-key-value-pairs-in-redis-1091ae80f74c
  [85]: https://www.infoq.com/presentations/twitch-pokemon/
  [86]: https://deliveroo.engineering/2016/10/07/optimising-session-key-storage.html
  [87]: https://deliveroo.engineering/2017/01/19/optimising-membership-queries.html
  [88]: https://github.com/JamzyWang/awesome-redis
  [89]: https://www.timescale.com/blog/time-series-data/
  [90]: https://www.timescale.com/blog/time-series-data-why-and-how-to-use-a-relational-database-instead-of-nosql-d0cd6975e87c/
  [91]: https://engineering.fb.com/2017/02/03/core-data/beringei-a-high-performance-time-series-storage-engine/
  [92]: https://netflixtechblog.com/introducing-atlas-netflixs-primary-telemetry-platform-bd31f4d8ed9a
  [93]: https://www.timescale.com/blog/when-boring-is-awesome-building-a-scalable-time-series-database-on-postgresql-2900ea453ee2/
  [94]: https://netflixtechblog.com/scaling-time-series-data-storage-part-i-ec2b6d44ba39
  [95]: https://leventov.medium.com/design-of-a-cost-efficient-time-series-store-for-big-data-88c5dc41af8e
  [96]: https://github.com/xephonhq/awesome-time-series-database
  [99]: https://graphdatabases.com/ 
  [100]: https://www.infoq.com/presentations/graph-database-scalability/
  [101]: https://neo4j.com/customers/
  [102]: https://blog.twitter.com/engineering/en_us/a/2010/introducing-flockdb
  [103]: https://architecht.io/google-ibm-back-new-open-source-graph-database-project-janusgraph-1d74fb78db6b
  [104]: https://aws.amazon.com/neptune/
  [105]: https://www.elastic.co/guide/en/elasticsearch/guide/master/index.html
  [106]: https://tech.ebayinc.com/engineering/elasticsearch-performance-tuning-practice-at-ebay/
  [107]: https://kickstarter.engineering/elasticsearch-at-kickstarter-db3c487887fc
  [108]: https://www.loggly.com/blog/nine-tips-configuring-elasticsearch-for-high-performance/
  [109]: https://medium.com/@abhidrona/elasticsearch-deployment-best-practices-d6c1323b25d7
  [110]: https://github.com/dzharii/awesome-elasticsearch

# 《MySQL 必知必会》分析笔记

## 第1章 存储：一个完整的数据存储过程是怎样的

### Q1：这一章的内容属于哪一类别

数据库/MySQL。

### Q2：这一章的内容是什么

介绍 MySQL 的数据存储过程。

### Q3：这一章的大纲是什么

- 创建 MySQL 数据库
- 确认字段
- 创建数据表
- 插入数据
- SQL 语句规范

### Q4：作者想要解决什么问题

作者想要解决以下问题：

- MySQL 是如何存储数据的？
- 如何把业务数据有序和高效地存储起来？

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

- 在 MySQL 中，一个完整的数据存储过程总共有 4 步，分别是创建数据库、确认字段、创建数据表、插入数据。

#### 创建 MySQL 数据库

注：以下 MySQL 命令均假设数据库名字为 demo，数据表名字为 test。

- 为啥我们要先创建一个数据库，而不是直接创建数据表呢？
  - 从系统架构的层次上看，MySQL 数据库系统从大到小依次是数据库服务器、数据库、数据表、数据表的行与列。
  - 数据库是 MySQL 里面最大的存储单元。
    数据表、数据表里的数据，以及我们以后会学到的表与表之间的关系，还有在它们的基础上衍生出来的各种工具，都存储在数据库里面。
    没有数据库，数据表就没有载体，也就无法存储数据。

- 数据库相关命令

  ```sql
  create database demo;
  show databases;
  # select certain database
  use demo;
  ```

- MySQL 系统自带数据库
  - 如果需要监控 MySQL 数据库各项性能指标、直接操作 MySQL 数据库系统文件等，可以由 DBA 通过 SQL 语句，查看 MySQL 系统自带数据库。
  - information_schema: 主要保存 MySQL 数据库服务器的系统信息，比如数据库的名称、数据表的名称、字段名称、存取权限、数据文件所在的文件夹和系统使用的文件夹等等。
  - performance_schema: 可以用来监控 MySQL 的各类性能指标。
  - sys: 主要作用是以一种更容易被理解的方式展示 MySQL 数据库服务器的各类性能指标，帮助系统管理员和开发人员监控 MySQL 的技术性能。
  - mysql: 数据库保存了 MySQL 数据库服务器运行时需要的系统信息，比如数据文件夹、当前使用的字符集、约束检查信息等等。

#### 创建数据表 & 确认字段

- 创建数据表的注意事项
  - 创建表的时候，最好指明数据库。否则，如果你没有选中数据库，Workbench 会提示错误；要是你当前选中的数据库不对，还可能把表创建到错误的数据库中。
  - 不要在最后一个字段的后面加逗号“,”，这也是初学者容易犯的错误。

- 数据库相关命令

  ```sql
  # show the structure of the table
  describe demo.test;
  show tables;
  ```

- 主键的特征
  - 必须唯一，不能重复；
  - 不能是空；
  - 必须可以唯一标识数据表中的记录。

- 主键使用规范
  - 建议一定要给表定义主键，并且养成习惯。因为主键可以帮助你减少错误数据，并且提高查询的速度。
  - 如果数据表中所有的字段都有重复的可能，可以添加一个不会重复的字段来做主键，比如自增整数。

- 字段名称建议用英文，原因有 2 个：一是书写方便；二是不容易出错。

#### 插入数据

- 添加数据时的注意事项
  - 插入数据一定要写上对应的字段名。这样做的好处是可读性好，不易出错，而且容易修改。否则，如果你记不住表的字段，就只能去查表的结构，才能知道值所对应的字段了。
  - 由于字段 itemnumber 定义了 AUTO_INCREMENT，所以我们插入一条记录的时候，不给它赋值，系统也会自动给它赋值。而且，每次赋值，都会在上次的赋值基础上，自动增加 1。

#### SQL 语句的书写规范

- MySQL 以分号来识别一条 SQL 语句结束，所以，你写的每一条 SQL 语句的最后，都必须有一个分号，否则，MySQL 会认为这条语句没有完成，提示语法错误。

- [SQL Style Guide][1]。

- [SQL 样式指南][2]。

- [Learn SQL: Naming Conventions][3]。

- 书籍：《SQL Programming Style》

  [1]: https://www.sqlstyle.guide/
  [2]: https://www.sqlstyle.guide/zh/
  [3]: https://www.sqlshack.com/learn-sql-naming-conventions/

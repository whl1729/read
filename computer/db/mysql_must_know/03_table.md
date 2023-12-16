# 《MySQL 必知必会》教程分析笔记

## 第3章 表：怎么创建和修改数据表

### Q1：这一章的内容属于哪一类别

数据库/MySQL。

### Q2：这一章的内容是什么

介绍数据表的基本操作，包括创建和修改数据表等。

### Q3：这一章的大纲是什么

- 如何创建数据表？
- 都有哪些约束？
- 如何修改表？
  - 添加字段
  - 修改字段

### Q4：作者想要解决什么问题

怎么创建和修改数据表？

### Q5：这一章的关键词是什么

### Q6：这一章的关键句是什么

#### 都有哪些约束

- 约束
  - 在 MySQL 创建表的语法结构里面，有一个词叫做「约束」。「约束」限定了表中数据应该满足的条件。
  - MySQL 会根据这些限定条件，对表的操作进行监控，阻止破坏约束条件的操作执行，并提示错误，从而确保表中数据的唯一性、合法性和完整性。

- 数据表的约束
  - 默认约束（DEFAULT）：即默认值约束。
  - 主键约束（PRIMARY）
  - 外键约束（FOREIGN KEY）：涉及表与表之间的关联，以及确保表的数据一致性的问题。
  - 非空约束（NOT NULL）
  - 唯一性约束（UNIQUE）：跟主键约束相比，唯一性约束要更加弱一些。
  - 自增约束（AUTO_INCREMENT）：可以让 MySQL 自动给字段赋值，且保证不会重复，非常有用。

- 主键约束 vs 唯一性约束
  - 在一个表中，我们可以指定多个字段满足唯一性约束，而主键约束则只能有一个，这也是 MySQL 系统决定的。
  - 满足主键约束的字段，自动满足非空约束，但是满足唯一性约束的字段，则可以是空值。

- 自增约束
  - 在数据表中，只有整数类型的字段（包括 TINYINT、SMALLINT、MEDIUMINT、INT 和 BIGINT），才可以定义自增约束。
  - 自增约束的字段，每增加一条数据，值自动增加 1.
  - 你可以给自增约束的字段赋值，这个时候，MySQL 会重置自增约束字段的自增基数，下次添加数据的时候，自动以自增约束字段的最大值加 1 为新的字段值。

#### 如何修改表

- 复制数据表

  ```sql
  CREATE TABLE demo.importheadhist
  LIKE demo.importhead;
  ```

- 添加字段

  ```sql
  ALTER TABLE demo.importheadhist
  ADD confirmer INT;


  ALTER TABLE demo.importheadhist
  ADD suppliername TEXT AFTER supplierid;
  ```

- 修改字段
  - MODIFY COLUMN does everything CHANGE COLUMN can, but without renaming the column.

  ```sql
  ALTER TABLE demo.importheadhist
  CHANGE quantity importquantity DOUBLE;

  ALTER TABLE demo.importheadhist
  MODIFY importquantity DECIMAL(10,3);
  ```

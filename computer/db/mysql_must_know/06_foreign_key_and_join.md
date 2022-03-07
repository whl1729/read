# 《MySQL 必知必会》教程分析笔记

## 第6章 外键和连接：如何做关联查询

### Q1：这一章的内容属于哪一类别？

数据库/MySQL。

### Q2：这一章的内容是什么？

介绍数据库外键、连接、关联查询的基础知识。

### Q3：这一章的大纲是什么？

- 如何创建外键？
- 连接
- 关联查询的误区

### Q4：作者想要解决什么问题？

如何做关联查询？

### Q5：这一章的关键词是什么？

- 外键
- 关联查询

### Q6：这一章的关键句是什么？

#### 外键

- 外键就是从表中用来引用主表中数据的那个公共字段
  - 假设我们有 2 个表，分别是表 A 和表 B，它们通过一个公共字段`id`发生关联关系，我们把这个关联关系叫做 R。
  - 如果`id`在表 A 中是主键，那么，表 A 就是这个关系 R 中的主表。相应的，表 B 就是这个关系中的从表。
  - 表 B 中的`id`，就是表 B 用来引用表 A 中数据的，叫外键。

- 外键约束
  - 在 MySQL 中，外键是通过外键约束来定义的。
  - 外键约束就是约束的一种，它必须在从表中定义，包括指明哪个是外键字段，以及外键字段所引用的主表中的主键字段是什么。
  - MySQL 系统会根据外键约束的定义，监控对主表中数据的删除操作。
    如果发现要删除的主表记录，正在被从表中某条记录的外键字段所引用，MySQL 就会提示错误，从而确保了关联数据不会缺失。

- 在创建表的时候定义外键约束

  ```sql
  [CONSTRAINT <foreign_constraint_name>] FOREIGN KEY field_name
  REFERENCES <main_table_name> field_name;
  ```

- 通过修改表来定义外键约束

  ```sql
  ALTER TABLE <slave_table_name> constrait_name FOREIGN KEY field_name
  REFERENCES main_table_name (field_name);
  ```

- 查看外键约束

  ```sql
  SELECT
    constraint_name,
    table_name,
    column_name,
    referenced_table_name,
    referenced_column_name
  FROM
    information_schema.KEY_COLUMN_USAGE
  WHERE
    constraint_name = 'fk_importdetails_importhead';
  ```

#### 连接

- 在 MySQL 中，有 2 种类型的连接，分别是内连接（INNER JOIN）和外连接（OUTER JOIN）。
  - 内连接表示查询结果只返回符合连接条件的记录，这种连接方式比较常用；
  - 外连接则不同，表示查询结果返回某一个表中的所有记录，以及另一个表中满足连接条件的记录。

- 在 MySQL 里面，关键字 JOIN、INNER JOIN、CROSS JOIN 的含义是一样的，都表示内连接。

- 外连接包括两类，分别是左连接和右连接。
  - 左连接，一般简写成 LEFT JOIN，返回左边表中的所有记录，以及右表中符合连接条件的记录。
  - 右连接，一般简写成 RIGHT JOIN，返回右边表中的所有记录，以及左表中符合连接条件的记录。

- 连接语句的语法结构

  ```sql
  /* join */
  SELECT column_name
  FROM table_name AS a
  JOIN table_name AS b
  ON (a.column_name = b.column_name);

  /* left join */
  SELECT column_name
  FROM table_name AS a
  LEFT JOIN table_name AS b
  ON (a.column_name=b.column_name);

  /* right join */
  SELECT column_name
  FROM table_name AS a
  RIGHT JOIN table_name AS b
  ON (a.column_name=b.column_name);
  ```

#### 关联查询的误区

- 多表查询
  - 把分散在多个不同的表里的数据查询出来的操作，就是多表查询。
  - 多表查询时，需要建立起多个表之间的关联，然后才能去查询，这便是「关联查询」。

- 关联查询
  - 误区：在 MySQL 中，外键约束不是关联查询的必要条件。很多人往往在设计表的时候，觉得只要连接查询就可以搞定一切了，外键约束太麻烦，没有必要。
  - 解释：虽然你不用外键约束，也可以进行关联查询，但是有了它，MySQL 系统才会保护你的数据，避免出现误删的情况，从而提高系统整体的可靠性。

- 大并发场景可能不适合使用外键约束
  - 原因：外键约束是有成本的，需要消耗系统资源。对于大并发的 SQL 操作，有可能会不适合。
    比如大型网站的中央数据库，可能会因为外键约束的系统开销而变得非常慢。
  - 解决方案：MySQL 允许你不使用系统自带的外键约束，在应用层面完成检查数据一致性的逻辑。
    也就是说，即使你不用外键约束，也要想办法通过应用层面的附加逻辑，来实现外键约束的功能，确保数据的一致性。

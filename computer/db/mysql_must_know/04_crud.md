# 《MySQL 必知必会》教程分析笔记

## 第4章 增删改查：如何操作表中的数据？

### Q1：这一章的内容属于哪一类别？

数据库/MySQL。

### Q2：这一章的内容是什么？

介绍对表中的数据增删改查的操作。

### Q3：这一章的大纲是什么？

- 添加数据
  - 插入数据记录
  - 插入查询结果
- 删除数据
- 修改数据
- 查询数据

### Q4：作者想要解决什么问题？

如何操作表中的数据？

### Q5：这一章的关键词是什么？

- ON DUPLICATE
- GROUP BY
- ORDER BY
- LIMIT

### Q6：这一章的关键句是什么？

#### 添加数据

- 在插入一条数据记录的时候，必须要考虑字段约束的 3 种情况。
  - 情况1：如果字段允许为空，而我们没有给它赋值，那么 MySQL 会自动给它们赋予空值。
  - 情况2：如果字段是主键，就不能为空，这个时候，MySQL 会按照我们添加的约束进行处理。
    比如字段`itemnumber`是主键，不能为空，而我们定义了自增约束，所以 MySQL 自动在之前的最大值基础上加了 1。
  - 情况3：如果有一个字段定义不能为空，又不是主键，当你插入一条数据记录的时候，就必须给这个记录赋值。

- 部分插入一条数据记录是可以的，但前提是
  - 没有赋值的字段，一定要让 MySQL 知道如何处理，比如可以为空、有默认值，或者是自增约束字段，等等，否则，MySQL 会提示错误的。

- MySQL 支持把查询的结果插入到数据表中，我们可以指定字段，甚至是数值，插入到数据表中。
  - 如果我们把查询的结果插入到表中时，导致主键约束或者唯一性约束被破坏了，就可以用`ON DUPLICATE`关键字进行处理。
  - `ON DUPLICATE`的作用是，告诉 MySQL，如果遇到重复的数据，该如何处理。

  ```sql
  INSERT INTO demo.goodsmaster
  SELECT *
  FROM demo.goodsmaster1 as a
  ON DUPLICATE KEY UPDATE barcode = a.barcode,goodsname=a.goodsname;
  ```

- 插入数据记录语句的语法结构

  ```sql
  INSERT INTO demo.goodsmaster
  (barcode, goodsname, price)
  VALUES
  ('0004', 'book', 30.00)
  ```

- 插入查询结果语句的语法结构

  ```sql
  INSERT INTO table_name (field_name)
  SELECT field_name_or_value
  FROM table_name
  WHERE condition
  ```

#### 删除数据

- 我们要习惯在删除数据的时候，添加条件语句 WHERE，防止误操作。

- 删除数据语句的语法结构
-
  ```sql
  DELETE FROM table_name
  WHERE condition
  ```

#### 修改数据

- 注意： **不要修改主键字段的值。** 因为主键是数据记录的唯一标识，如果修改了主键的值，就有可能会破坏数据的完整性。

- 修改数据语句的语法结构

  ```sql
  UPDATE table_name
  SET field_name=field_value
  WHERE condition
  ```

#### 查询数据

- 查询数据语句的语法结构

  ```sql
  SELECT *|field_list
  FROM data_source
  WHERE condition
  GROUP BY field
  HAVING condition
  ORDER BY field
  LIMIT start_line, line_num
  ```

- `FROM`
  - FROM 关键字后面，还可以跟着更复杂的数据表联接。
  - 数据源也不一定是表，也可以是一个查询的结果。

- `ORDER BY`
  - 作用是告诉 MySQL 查询结果如何排序。ASC 表示升序，DESC 表示降序。

- `GROUP BY`
  - 作用是告诉 MySQL 查询结果要如何分组，经常与 MySQL 的聚合函数一起使用。

- `LIMIT`
  - 作用是告诉 MySQL 只显示部分查询的结果。MySQL 中，起始位置的起点是 0.

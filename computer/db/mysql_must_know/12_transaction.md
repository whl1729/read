# 《MySQL 必知必会》教程分析笔记

## 第12章 事务：怎么确保关联操作正确执行？

### Q1：这一章的内容属于哪一类别？

数据库/MySQL。

### Q2：这一章的内容是什么？

介绍数据库事务的基础知识。

### Q3：这一章的大纲是什么？

- 什么是事务？
- 如何确保操作的原子性和数据的一致性？
- 如何用好事务的隔离性？
- 总结

### Q4：作者想要解决什么问题？

- 什么是事务？
- 如何正确使用事务？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 什么是事务？

- 事务的定义
  - 事务是 MySQL 的一项功能，它可以使一组数据操作（也叫 DML 操作），要么全部执行，要么全部不执行，
    不会因为某种异常情况（比如硬件故障、停电、网络中断等）出现只执行一部分操作的情况。

> 备注：DML 是英文 Data Manipulation Language 的缩写，包括 SELECT、INSERT、UPDATE 和 DELETE.

- 事务的语法结构

  ```sql
  /* 开始事务 */
  START TRANSACTION or BEGIN
  /* 一组DML语句 */
  ...
  /* 提交事务 */
  COMMIT

  /* 事务回滚 */
  ROLLBACK
  ```

- 事务 SQL 语句的关键字
  - `START TRANSACTION` 和 `BEGIN`：表示开始事务，意思是通知 MySQL，后面的 DML 操作都是当前事务的一部分。
  - `COMMIT`：表示提交事务，意思是执行当前事务的全部操作，让数据更改永久有效。
  - `ROLLBACK`：表示回滚当前事务的操作，取消对数据的更改。

- 事务的4个主要特征：ACID
  - 原子性（atomicity）：表示事务中的操作要么全部执行，要么全部不执行，像一个整体，不能从中间打断。
  - 一致性（consistency）：表示数据的完整性不会因为事务的执行而受到破坏。
  - 隔离性（isolation）：表示多个事务同时执行的时候，不互相干扰。不同的隔离级别，相互独立的程度不同。
  - 持久性（durability）：表示事务对数据的修改是永久有效的，不会因为系统故障而失效。

#### 如何确保操作的原子性和数据的一致性？

- 错误处理
  - 事务并不会自动帮你处理 SQL 语句执行中的错误，如果你对事务中的某一步数据操作发生的错误不做处理，继续提交的话，仍然会导致数据不一致。
  - 如果发现事务中的某个操作发生错误，要及时使用回滚；
  - 只有事务中的所有操作都可以正常执行，才进行提交。
  - 我们可以在 MySQL 的存储过程中，通过获取 SQL 错误，来决定事务是提交还是回滚：

  ```sql
  mysql> DELIMITER //                   -- 修改分隔符为 //
  mysql> CREATE PROCEDURE demo.mytest() -- 创建存储过程
  -> BEGIN                              -- 开始程序体
  -> DECLARE EXIT HANDLER FOR SQLEXCEPTION ROLLBACK; -- 定义SQL操作发生错误是自动回滚
  -> START TRANSACTION;                              -- 开始事务
  -> INSERT INTO demo.mytrans VALUES (1,5);
  -> UPDATE demo.inventory SET invquantity = invquantity - 5;
  -> COMMIT;                                         -- 提交事务
  -> END
  -> //                                              -- 完成创建存储过程
  Query OK, 0 rows affected (0.05 sec)

  mysql> DELIMITER ;                                 -- 恢复分隔符为；
  mysql> CALL demo.mytest();                         -- 调用存储过程
  Query OK, 0 rows affected (0.00 sec)

  mysql> SELECT * FROM demo.mytrans;                 -- 销售流水没有插入
  Empty set (0.00 sec)
  mysql> SELECT * FROM demo.inventory;               -- 库存也没有消减，说明事务回滚了
  ```

- 结束标识
  - `DELIMITER //`语句把MySQL 语句的结束标识改为`//`（默认语句的结束标识是`;`）
  - 这样做的目的是告诉 MySQL 一直到`//`才是语句的结束，
    否则，MySQL 会在遇到第一个`;`的时候认为语句已经结束，并且执行，这样就会报错。

- 事务使用要点
  - 我们要把重要的关联操作放在事务中，确保操作的原子性，并且对失败的操作进行回滚处理。
  - 只有这样，才能真正发挥事务的作用，保证关联操作全部成功或全部失败，最终确保数据的一致性。

#### 如何用好事务的隔离性？

- MySQL 可以用锁来控制事务对数据的操作，从而实现事务之间的相互隔离。锁的使用方式不同，隔离的程度也不同。

- MySQL 支持 4 种事务隔离等级
  - `READ UNCOMMITTED`：可以读取事务中还未提交的被更改的数据。
  - `READ COMMITTED`：只能读取事务中已经提交的被更改的数据。
  - `REPEATABLE READ`：表示一个事务中，对一个数据读取的值，永远跟第一次读取的值一致，不受其他事务中数据操作的影响。这也是 MySQL 的默认选项。
  - `SERIALIZABLE`：表示任何一个事务，一旦对某一个数据进行了任何操作，那么，一直到这个事务结束，MySQL 都会把这个数据锁住，禁止其他事务对这个数据进行任何操作。

- 事务隔离等级的选择
  - 等级越高，消耗的系统资源也越多，你要根据实际情况进行设定。
  - 一般来讲，使用 MySQL 默认的隔离等级 REPEATABLE READ，就已经够了。
  - 不过，也不排除需要对一些关键的数据操作，使用最高的隔离等级 SERIALIZABLE。

#### 总结

- 在 MySQL 中，并不是所有的操作都可以回滚。
  - 比如创建数据库、创建数据表、删除数据库、删除数据表等，这些操作是不可以回滚的。
  - 所以，你在操作的时候要特别小心，特别是在删除数据库、数据表时，最好先做备份，防止误操作。
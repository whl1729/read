# Fluent Python 分析笔记

## 13 Interfaces, Protocols, and ABCs

### 这一章的大纲是什么

- 鸭子类型（duck typing） 和 静态鸭子类型（static duck typing, e.g., typing.Protocol）的对比
- 深入解析鸭子类型
- 鹅类型（Goose Typing, e.g., ABC）的用法
- 静态协议的用法、实现和设计

### 目前为止我知道什么

- 鸭子类型是指：你实现了一些接口，就能享用为实现这个接口的所有类型定义的各种功能，包括迭代、元素索引等
- 静态鸭子类型是指：你可以为某种对象加上类型约束，说明它要支持哪些协议，比如 lessThan 等。

### 目前为止我不知道什么

- 鹅类型（ABC）的用法是怎样的
- 静态协议是什么意思？其用法、实现和设计是怎样的

### 这一章的主要内容是什么
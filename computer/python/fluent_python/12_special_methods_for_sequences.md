# Fluent Python 分析笔记

## 12 Special Methods for Sequences

### 这一章的大纲是什么

这一章要将 Vector2d 拓展到更高维度的 Vector，并且支持以下功能：

- 基本的序列协议：`__len__` 和 `__getitem__`
- 含有许多元素的实体的安全表示
- 支持切片，并输出新的 Vector 实体
- Aggregate hashing
- 自定义格式化语言插件

### 目前为止我知道什么

不妨将 Vector2d 拓展到更高维度的类就叫做 Vector。
Vector 内部可以用一个 array 来存储元素。
目前我知道如何支持以下功能：

- `__len__`：返回 Vector 内部 array 的元素数目。
- `__getitem__`：返回 Vector 内部 array 特定索引的元素。
- 切片：先对 Vector 内部 array 求切片，然后调用 Vector 的构造函数返回 Vector。

### 目前为止我不知道什么

- 「含有许多元素的实体的安全表示」是什么？
- Aggregate hashing 是什么？
- 「自定义格式化语言插件」是什么？

### 这一章的主要内容是什么

# Fluent Python 分析笔记

## 5 Data Class Builders

### 这一章的大纲是什么

- collections.namedtuple
- typing.NamedTuple
- @dataclasses.dataclass
- 数据类往往体现了代码坏味道

### 目前为止我知道什么

- 这一章的3种数据类构造器我都不了解。
  以前我需要构造一个数据类的时候，一般是这样写的：

```python
class Data:
  def __init__(self, a, b, c):
    self.a = a 
    self.b = b 
    self.c = c
```

- Tuple 是元祖，访问元祖的元素时跟访问列表的元素类似，使用下标即可：`x[0]`。
- NamedTuple 指元祖的每个元素都有名字，可以通过名字来访问：`x.foo`。

- 「数据类往往体现了代码坏味道」这个观点不太理解，是说封装性不够，应该尽量把数据相关的操作也定义在类里面吗？

### 目前为止我不知道什么

- collections.namedtuple
- typing.NamedTuple
- @dataclasses.dataclass
- 数据类往往体现了代码坏味道

### 这一章的主要内容是什么

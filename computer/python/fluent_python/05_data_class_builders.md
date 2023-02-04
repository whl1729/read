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

- 简单定义的数据类的问题
  - 从 `object` 继承的 `__repr__` 方法没啥用（打印类时只会显示 ID 信息）
  - 从 `object` 继承的 `__eq__` 方法也没啥用（通过比较 ID 来判断是否相等）
  - 因此想要比较两个数据类对象的取值时，需要显式比较这两个对象的每一个成员

- collections.namedtuple

  ```python
  from collections import namedtuple
  Coordinate = namedtuple('Coordinate', 'lat lon')
  ```

- typing.NamedTuple

  ```python
  import typing
  Coordinate = typing.NamedTuple('Coordinate', [('lat', float), ('lon', float)])
  ```

- @dataclasses.dataclass

  ```python
  from dataclasses import dataclass

  @dataclass(frozen=True)
  class Coordinate:
    lat: float
    lon: float

    def __str__(self):
      ns = 'N' if self.lat >= 0 else 'S'
      we = 'E' if self.lon >= 0 else 'W'
      return f'{abs(self.lat):.1f}°{ns}, {abs(self.lon):.1f}°{we}'
  ```

- @dataclasses.dataclass 可以定义 `__post__init__`

  ```python
  from dataclasses import dataclass
  from club import ClubMember

  @dataclass
  class HackerClubMember(ClubMember):
    all_handles = set()
    handle: str = ''

    def __post_init__(self):
      cls = self.__class__
      if self.handle == '':
        self.handle = self.name.split()[0]
  ```

- 数据类往往体现了代码坏味道
  - 数据类对外暴露了太多细节（一个类应该将数据和行为封装在一起）
  - 数据类可能会导致调用方出现重复代码

### 这一章的知识本质、第一原则和结构是什么

这一章主要介绍了数据类，其本质就是一个用于存储数据、缺少封装的类。

我认为这一章的知识的第一原则是慎用和少用数据类。

这一章的知识结构是三种数据类的用法，分别是 collections.namedtuple, typing.NamedTuple 和 dataclasses.dataclass。
其中 dataclasses.dataclass 最灵活，可以定义 `__str__` 或 `__post_init__` 等方法。
实践中根据实际需求选用三种之一即可，当然别忘了第一原则——慎用和少用数据类。

# Fluent Python 分析笔记

## 1 The Python Data Model

参考：[The "Data Model" chapter of The Python Language Reference][1]

### 第1章的主要内容是什么

- 一致性
  - Python 最好的特点之一是一致性。

- 数据模型
  - 如果将 Python 语言视为一个框架
  - 那么数据模型就是对这个框架的描述
  - 具体地说，数据模型描述了 Python 这个框架各个组件的接口
  - 包括序列、函数、类、迭代器、协程、上下文管理器等
  - 比如：序列有 `__len__` 接口，类有 `__init__` 接口等

- 特殊方法
  - 名字前后各有两个下划线
  - 用来提供基本的对象操作
  - 特殊方法是用来给 Python 解析器调用的，而非用户调用的
  - `len(collection)` 实际上是调用 `collection.__len__()`
  - `obj[key]` 实际上是调用 `obj.__getitem__()`
  - `for i in x` 实际上是调用 `x.__iter__()` 或 `x.__getitem__()`
  - `value in collection` 实际上是调用 `collection.__contains__` 或者是顺序遍历

- 特殊方法的使用场景
  - 集合
  - 属性访问
  - 迭代
  - 运算符重载
  - 函数和方法调用
  - 字符串表示和格式化
  - 异步编程
  - 对象创建和销毁
  - 上下文管理

- 特殊方法的四个常用场景
  - 模仿数字类型（运算符重载）：`__abs__`, `__add__`, `__mul__`
  - 字符串表示：`__repr__`, `__str__`
  - 自定义类型的布尔值判断：`__bool__`, `__len__`
  - Collection API: `__iter__`, `__len__`, `__contains__`

  ![collection_types_uml](images/collection_types_uml.jpg)

  ![special_method_names_operators_excluded](images/special_method_names_operators_excluded.jpg)

  ![special_method_names_and_symbols_for_operators](images/special_method_names_and_symbols_for_operators.jpg)

### 第1章的本质是什么

第1章介绍了一项我之前没了解的知识：Python 数据模型。
我认为这项知识的本质就是接口，运用的是面向对象编程的思想。
它的第一原则就是定义特殊方法来实现接口，比如定义了`__repr__` 就实现了字符串表示接口。
它的知识框架就是一大堆特殊方法，这些特殊方法存在一些继承关系。

Go 语言同样是面向接口编程模式，只是 Go 定义接口一般需要明确定义 `type interface xxx`，
而 Python 似乎默认帮你定义了很多底层接口，你直接实现就可以用了。

两个例子：

```python
class Foo:
  def __getitem__(self, i):
      return i ** 2

foo = Foo()
# 以下循环不会结束，这意味着我们构造了一个无穷数组
for i in foo:
    print(i)
```

```python
class Bar:
  def __init__(self):
      self._len = 0

  def __len__(self):
      self._len += 1
      return self._len

bar = Bar()
for i in range(10):
    # 每次循环会导致len(bar)增加1. 这意味着我们伪造了一个长度不断增加的对象。
    print(len(bar))
```

  [1]: https://docs.python.org/3/reference/datamodel.html

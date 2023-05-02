# Fluent Python 分析笔记

## 22 Dynamic Attributes and Properties

### 第22章讨论哪些内容

- 动态属性的两种实现方式
  - `@property` 装饰器
  - `__getattr__` 特殊函数

- 虚拟属性：通过 `__getattr__` 来实现

- property
  - 可计算的属性
  - 使用 property 来校验属性合法性
  - property 的内部实现
  - 实现 property 工厂

- 处理属性删除

- 处理属性相关的基础属性和函数

### 目前为止我知道什么

- Python 属性包括数据和函数，并且可以动态添加

### 目前为止我不知道什么

- `__getattr__` 的作用和用法
- `@property` 的作用、用法和实现
- Python 属性删除
- Python 处理属性的相关基础属性和函数

### 第22章的主要内容有哪些

- Uniform Access Principle (by Bertrand Meyer)

  > All services offered by a module should be available through a uniform notation,
  > which does not betray whether they are implemented through storage or through computation.

### 第22章的知识如何指导实践

- Example 22-4 的 FrozenJSON 通过定义 `__getattr__` 方法，将方括号访问转为点访问，使用更方便。（但性能可能有所下降）

- Example 22-4 的 FrozenJSON 通过定义 `__dir__` 方法，可以方便 IDE 自动保全。

- Example 22-9 提供了一种将输入参数转为类属性的快捷方式：

  ```python
  def __init__(self, **kways):
      self.__dict__.update(kwargs)
  ```

- Example 22-12 通过 `self.__class__.fetch` 的方式调用函数，以避免数据集字段与类属性冲突。

- Example 22-13 `cls_name = record_type.capitalize()` 使用 `capitalize` 来将字符串首字母转为大写形式。

- Example 22-14 通过对象的 `__dict__` 来读写数据，避免无限递归。

  ```python
  @property
  def speakers(self):
      spkr_serials = self.__dict__['speakers']
  ```

- Example 22-21 介绍了通过 `@property` 在不改变属性名字的情况下对属性增加校验的机制

- Example 22-23 介绍了实体的属性会屏蔽类的属性，定义类的属性时要注意这一点。

- "Flexible Object Creation with __new__" 一节提到 Python 的构造器其实是 `__new__`，而 `__init__` 只是初始化函数。

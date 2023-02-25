# Fluent Python 分析笔记

## 11 A Pythonic Object

### 这一章的大纲是什么

- 对象类型转换方法，如 `repr()`, `bytes()`, `complex()` 等
- 实现一个可替代的构造函数
- 拓展格式化字符串
- 设置属性权限为只读
- 使对象可哈希化
- 使用 `__slots__` 来优化内存
- 使用 `@classmethod` 和 `@staticmethod`
- Python 私有属性和受保护属性的用法与局限性

### 目前为止我知道什么

- 如果没有为对象定义特殊方法，对象的打印信息不太友好，类似 `<__main__.Foo object at 0x7ff9b07b79d0>`。
- 如果想自定义对象的打印格式，可以为其定义 `__repr__()` 或 `__str__()` 。如果只想定义一个方法，可以只定义 `__repr__()`。
- 对象默认可哈希化。如果没有为对象定义特殊方法，对象的每个实体的哈希化结果都不一样。
- 如果想自定义对象的哈希化结果，可以为其定义 `__hash__()` 和 `__eq__()`。
- `@staticmethod` 用于在对象里定义不需要 `self` 作为输入参数的函数。
- `@classmethod` 应该是为对象本身定义的函数，该函数在内存中只保存一份，由所有实体共享。单例模式（singleton）时好像用到这个。
- Python 似乎没有将属性设置为私有或受保护的方法？

### 目前为止我不知道什么

- `bytes()` 和 `complex()` 的实现方法和使用场景是什么？
- 实现一个可替代的构造函数是啥意思？比如 `array.frombytes()` 方法，就是从其他类型构造出目标类型。
- 如何拓展格式化字符串？
- 如何设置属性权限为只读？
- 如何使用 `__slots__` 来优化内存？
- 如何使用 `@classmethod`？
- Python 私有属性和受保护属性的用法与局限性是什么？

### 这一章的主要内容是什么

- `__repr__` vs `__str__`
  - `__repr__` 是为了消除含糊性（提供实体需要知道的所有信息），`__str__` 是为了可读性
  - `__repr__` 主要用于调试和开发，`__str__` 主要用于打印输出
  - 如果只定义了 `__repr__`，那么 `__str__ = __repr__`
  - 如果同时定义了 `__repr__` 和 `__str__`，那么两者互不影响

  ```python
  >>> class Cat:
  >>>     def __init__(self, name):
  >>>         self.name = name
  >>>     def __repr__(self):
  >>>         return f'Cat(name={self.name})'
  >>>     def __str__(self):
  >>>         return self.name
  >>>

  >>> cat = Cat('ali')

  >>> cat
  >>> Cat(name=ali)

  >>> f'{cat}'
  >>> 'ali'

  >>> print(cat)
  >>> 'ali'

  >>> s =set([cat])

  >>> s
  >>> {Cat(name=ali)}

  >>> print(s)
  >>> {Cat(name=ali)}
  ```

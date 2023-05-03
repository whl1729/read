# Fluent Python 分析笔记

## 24 Class Metaprogramming

### 第24章讨论哪些话题

- 类是一等对象
- 类装饰器
- 元类

### 目前为止我知道什么

- Python 类具有属性、特殊函数等内容
- 函数装饰器是一个函数，将原函数「装饰」成另一个函数；
  类装饰器也是一个函数，将原类「装饰」成另一个类。

### 目前为止我不知道什么

- 类和对象有何区别
- 有哪些类装饰器
- 元类的概念和用法

### 第24章的主要内容是什么

- Python 魔法
  - `object` is an instance of `type`
  - `type` is a subclass of `object`
  - `type` is an instance of itself

- 自定义元类 `MetaKlass` 执行顺序
  - 执行 `MetaKlass.__new__`，里面可能会调用 `super().__new__`
  - 执行 `SuperKlass.__init__subclass__`，输入参数为刚创建的 class
  - 如果定义了类装饰器，则执行之
  - 将类对象与命令空间中的类名绑定

### 如何拓展第24章的内容

- `type.__new__` 函数实现了类的构造过程，是通过C语言实现的。
- The Python Language Reference, "Data Model", "3.3.3. Customizing class creation"

### 关于第24章我有哪些疑问

- 类、对象和类型的区别是什么

### 第24章如何指导实践

- Example 24-9 通过 plural 变量来判断是否加复数：`plural = 's' if len(names_ > 1 else '')`

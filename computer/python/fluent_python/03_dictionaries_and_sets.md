# Fluent Python 分析笔记

## 3 Dictionaries and Sets

### 这一章的大纲是什么？

- 创建和处理 dict 和映射的语法，包括解包和模式匹配
- 映射类型的常用方法
- key 不存在时的特殊处理
- dict 的变体
- set 和 frozenset 类型
- 哈希表对集合或字典的行为的影响

### 目前为止我知道什么？

- 创建 dict: `people = {'name': 'guojing', 'age': 20}`
- dict 的部分常用方法：`d[key]`, `d.get(key, def_val)`
- dict 的 key 不存在时的特殊处理：好像可以定义 `__miss__` 函数，但不熟悉
- dict 有这些变体：collections 库有 ChainMap、OrderedDict、UserDict、defaultdict 等变体，但不熟悉
- 创建 set：`people = {'guojing', 'huangrong'}`

### 目前为止我不知道什么？

- dict 解包和模式匹配
- dict 的其他常用方法
- dict 的 key 不存在时的特殊处理
- dict 的变体的具体用法
- frozenset 的语法
- 哈希表对集合或字典的行为的影响

### 这一章的主要内容是什么？

- `__builtins__.__dict__` 存储了所有的内建类型、对象和函数。

- dict 解包
  - 在函数参数中可以使用 `**` 来对多个字典变量解包
  - 在 dict 字面量中也可以使用 `**` 来对字典变量解包

  ```python
  def dump(**kwargs):
    return kwargs

  dump(**{'x': 1}, y=2, **{'z': 3})
  ```

  ```python
  {'a': 0, **{'x': 1}, 'y': 2, **{'z': 3, 'x': 4}}
  ```

- dict 模式匹配
  - 支持部分匹配，也可以使用 `**extra` 来匹配剩余键值对

  ```python
  def get_creators(record: dict) -> list:
      match record:
          case {'type': 'book', 'api': 2, 'authors': [*names]}:
              return names
          case {'type': 'book', 'api': 1, 'author': name}:
              return [name]
          case {'type': 'book'}:
              raise ValueError(f"Invalid 'book' record: {record!r}")
          case {'type': 'movie', 'director': name}:
              return [name]
          case _:
              raise ValueError(f"Invalid record: {record!r}")
  ```

- dict 常用方法
  - 增：update
  - 删：clear, pop, popitem
  - 查：get, keys, values, items
  - 改：update, setdefault

- dict 的 key 不存在时的处理方法
  - setdefault: `my_dict.setdefault(key, []).append()`
  - defaultdict: `index = collections.defaultdict(list)`
  - 自定义 dict 对象中增加定义 `__missing__` 方法

- dict 的变体
  - collections.OrderedDict: 判断相等时会比较插入顺序
  - collections.ChainMap: 特别适合模拟嵌套作用域
  - collections.Counter: 自动计数器
  - shelve.Shelf: 提供持久性保存方案，等需要用再查
  - collections.UserDict: 更适合用来派生自定义字典，比 dict 更方便

- frozenset
  - `fs = frozenset([30,40])`
  - frozenset 相比 set，少了 update 等方法，因为它不允许修改

- 哈希表对字典的行为的影响
  - Python 的 dict 是通过哈希表来实现的
  - Python 的 dict 的 key 必须是可哈希对象
  - Python 的 dict 的 key 是有序的，这是 CPython 3.6 内部实现带来的副作用

- 哈希表对哈希的行为的影响
  - Python 的 set 或 frozenset 也是通过哈希表来实现的
  - Python 的 set 元素必须是可哈希对象
  - Python 的 set 的元素顺序取决于插入顺序，不过是不稳定的（当出现两个 hash code 相同的元素时）
  - 添加元素可能会改变 Python 的 set 的排序，因为可能需要重新申请内存和移动数据

- 可哈希（hashable）
  - 定义了 `__hash__` 和 `__eq__` 方法

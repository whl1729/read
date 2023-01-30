# Fluent Python 分析笔记

## 4 Unicode Text Versus Bytes

### 第4章的主要内容是什么

- 处理文本文件
  - 最佳实践是：Unicode 三明治
  - 注意默认编码格式的陷阱，不要依赖默认编码格式，打开文件时显式声明编码格式
    - Windows 系统的默认编码格式不是 utf-8（我的 Windows 系统是 cp936）
    - 重定向 stdout 时，stdout 的编码格式会变为系统默认编码格式。（我的 Windows 系统下，会由 utf-8 变为 gbk）

- Unicode 三明治
  - 输入层：将字节流解码为字符串（bytes -> str)
  - 中间层：只处理字符串（100% str）
  - 输出层：将字符串编码为字节流（str -> bytes）

- 中文编码标准发展：GB2312 -> GBK -> CP936

- '\N{}' 可以表示 Unicode 字符，特别好玩

  ```python
  '\N{ANT}'
  '\N{BUTTERFLY}'
  '\N{CAT}'
  '\N{MONKEY}'
  '\N{OHM SIGN}'
  ```

- Unicode 字符的比较
  - Unicode 字符的标准化
    - Unicode 有组合字符，即普通字符后跟特殊字符（如变音字符），在打印时显示为1个字符。比如：'case\N{COMBINING ACUTE ACCENT}'
    - 组合字符的存在，使得 Unicode 单词可能有不止一种组合方式。
    - 使用 unicodedata.normalize 方法可以将 Unicode 字符串标准化。
  - Unicode 字符的大小写转换
    - `str.casefold()` 与 `str.lower()` 均是将字符转为小写形式
    - 大约有300个码点调用这两个函数转为小写时会返回不同的结果
  - 根据实际需要，可以先对 Unicode 字符进行标准化或大小写转换后，再比较大小

- Unicode 文本的排序
  - 直接使用 `sorted` 对非 ASCII 文本进行排序，可能结果会不正确。
  - 可以使用 `locale.strxfrm` 或 `pyuca` 来对 Unicode 文本进行排序。

- Unicode 数据库
  - 记录了码点到字符名字的映射关系、字符元数据（是否可打印、是否为字母、是否为数字等）
  - `unicodedata` 模块可以检索字符的元数据信息

- Unicode Dual-Mode str 和 bytes API
  - re 模块中，使用 bytes 构造的正则表达式和使用 str 构造的正则表达式，匹配行为会有差异。（前者 \d 和 \w 只会匹配 ASCII 字符）
  - os 模块中，所有函数接收文件名或路径名时，都支持 str 或 bytes 两种类型，以解决部分编码问题。

### 第4章的知识本质、第一原则和结构是什么

第4章介绍了 Unicode 文本与字节流，其本质是字符的编码/解码。

我认为第4章的知识的第一原则是：字符串与字节流的转化过程中涉及到编码/解码。

第4章的知识结构是：Unicode 的基本概念（字符、码点、字节表示、编码、解码）、处理编码错误、避免编码陷阱、文本处理最佳实践。
至于文本的比较、排序、标准化、大小写转换等，等实际使用时需要了解相关细节，目前知道有这个知识点即可。
另外需要注意接口对 str 与 bytes 的不同处理，避免踩坑。

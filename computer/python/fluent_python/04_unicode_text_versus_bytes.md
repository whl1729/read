# Fluent Python 分析笔记

## 4 Unicode Text Versus Bytes

### 第4章讨论哪些内容

- 字符、码点、字节表示
- 二进制序列的独有特性：bytes, bytearray, memoryview
- 全 Unicode 和字符集的编码
- 避免和处理编码错误
- 文本文件处理最佳实践
- 默认编码陷阱和标准I/O问题
- 安全的 Unicode 文本比较
- 规范化、大小写转换、暴力去除变音字符等通用函数
- 使用 locale 和 pyuca 库来对 Unicode 文本排序
- Unicode 数据库的字符元数据
- 处理 str 和 bytes 的 Dual-mode API

### 目前为止我知道什么

- 字符可以理解为文字的基本单元，比如英文字母、数字、标点符号、中文字符等。
- 码点是字符对应的数值，也就是字符编码的结果。（错了，码点是尚未编码的数值）
- 字节表示是指字符对应的码点的字节表示，一个码点可能由若干个字节来表示，视具体编码方式而定。
- Unicode 提供了一套字符与码点的映射方案？UTF-8、UTF-16 及 GB2312 等都是基于 Unicode 的编码方案？
- Python 在 Windows 系统容易出现编码问题，因为国内 Windows 系统的默认编码不是 utf-8，而是 GB2312 之类的。
- Python 在 Ubuntu 系统不容易出现编码问题，因为 Ubuntu 系统的默认编码是 utf-8.
- 如果担心出现编码错误，可以使用 `try ... except` 来捕捉异常。

### 目前为止我不知道什么

- bytes, bytearray, memoryview 的语法
- Unicode 与 UTF-8、GB 2312 等的联系与区别不太确定
- 如何避免和处理编码错误
- 文本文件处理最佳实践
- 默认编码陷阱和标准I/O问题
- 安全的 Unicode 文本比较
- 规范化、大小写转换、暴力去除变音字符等通用函数
- 使用 locale 和 pyuca 库来对 Unicode 文本排序
- Unicode 数据库的字符元数据
- 处理 str 和 bytes 的 Dual-mode API

### 第4章的主要内容是什么

- 字符、码点、字节表示
  - 字符一般指 Unicode 字符。Unicode 字符可以表示世界上大部分的文字和符号。
  - 在 Unicode 标准中，码点是一个取值在[0, 1114111]之间的数值，由 `U+` 和4到6个十六进制数字组成，即 U+0000 ~ U+10FFFF.
  - 字符的字节表示取决于编码方式，UTF-8、UTF-16 或 GB2312 等是不同的编码标准。

- 二进制序列的字面表示
  - 取值为 32 ~ 126 的字节，直接表示为对应的 ASCII 字符
  - 制表符、换行符、回车符和反斜杠，分别使用 `\t, \n, \r, \\` 来表示
  - 如果单双引号同时出现，整个序列使用单引号括起来，序列内部的单引号需要转义，即`\'`
  - 其他字节取值，采用十六进制转义序列来表示，比如`\x00`

- bytes vs bytearray
  - 相同点：均可用于二进制序列的表示
  - 不同点：bytes 不可修改，bytearray 可以修改

- 有些编码格式不能表示所有 Unicode 字符
  - ASCII 不能表示任何中文字符
  - GB2312 不能表示部分特殊字符

- 常见编码格式
  - utf-8 与 utf-16 的区别是，前者对每个字符的编码结果可以是1、2、3或4个字节，后者只会是2个或4个字节。
  - latin1 （也就是 iso8859_1）是 cp1252 和 Unicode 等编码格式的基础
  - cp1252 是微软发明的编码格式，是 latin1 的超集
  - cp437 是 IBM PC 的编码格式
  - gb2312 是中国大陆用于编码简体中文的编码格式，也是亚洲语言的常用编码格式之一

- 处理编码/解码错误
  - 字符串的 `encode` 方法提供参数 `errors`，可以指定如何处理 `UnicodeEncodeError`
  - 同理，二进制串的 `decode` 方法提供参数 `errors`，可以指定如何处理 `UnicodeDecodeError`
  - 特别注意，cp1252, iso8859_1 和 koi8_r 等编码标准可以解码任意二进制串，直接忽略随机噪音，不会报错

  ```python
  city = '深圳'
  city.encode('cp437')  # throws UnicodeEncodeError
  city.encode('cp437', errors='ignore')
  city.encode('cp437', errors='replace')
  city.encode('cp437', errors='xmlcharrefreplace')
  ```

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

### 我有哪些问题

#### Q1：输入法与编码格式之间的关系是什么

比如说，我有个文件，是 latin1 格式的，如果我在这个文件中输入中文，会怎么样？
参考资料：[文件和输入法的字符编码 - 东南西北风的文章 - 知乎][2]

这里需要区分文件数据的保存与文件新增输入数据的显示：

文件数据的保存取决于编辑器，保存时使用编辑器默认的编码格式，或者是用户显式指定的编码格式。
文件数据新增输入数据的显示取决于编辑器和操作系统，编辑器需要从操作系统中获取输入的信息，
并且需要调用操作系统接口来显示对应的输入内容。这个过程中双方的交互也需要对齐编码格式。

我在 Ubuntu 20.04 系统下的一些测试：

- 在 vim 中打开一个中文文档，输入`:set encoding=latin1`，出现大部分乱码
- 在 vim 中打开相同的中文文档，输入`:set encoding=gb2312`，出现大部分乱码
- 在 vim 中打开一个中文文档，输入`:set encoding=latin1`，出现大部分乱码后，继续输入中文，输入的中文依然是大部分乱码

### 参考资料

- [Character Encoding and Unicode in Python][1]

  [1]: https://www.youtube.com/watch?v=Mx70n1dL534
  [2]: https://zhuanlan.zhihu.com/p/487734866

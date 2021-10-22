# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 5: Basic Reference Type

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

#### 一级大纲

- The Date Type
- The RegExp Type
- Primitive Wrapper Type
- Singleton Built-in Objects

#### 二级大纲

- The Date Type
  - Inherited Methods
  - Date-Formatting Methods
  - Date/Time Component Methods
- The RegExp Type
  - RegExp Instance Properties
  - RegExp Instance Methods
  - RegExp Constructor Properties
  - Pattern Limitations
- Primitive Wrapper Type
  - The Boolean Type
  - The Number Type
  - The String Type
- Singleton Built-in Objects
  - The Global Object
  - The Math Object

### Q3：作者想要解决什么问题？

- Working with objects
- Understanding basic JavaScript data types
- Working with primitives and primitive wrappers

### Q4：这一章的关键词是什么？

- Reference value
- Reference Type
- Primitive Wrapper Type

### Q5：这一章的关键句是什么？

- Reference Value vs Reference Type
  - A reference value (object) is an instance of a specific reference type.
  - Reference types are also sometimes called object definitions
    because they describe the properties and methods that objects should have.
  - Functions are a reference type.

- Reference Type vs Class
  - In ECMAScript, reference types are structures used to group data and functionality together and are often incorrectly called classes.
  - Although technically an object-oriented language,
    ECMAScript lacks some basic constructs that have traditionally been associated with object-oriented programming,
    including classes and interfaces.

- Constructor
  - A constructor is simply a function whose purpose is to create a new object.
  - New objects are created by using the new operator followed by a constructor.

#### 5.1 The Date Type

- Date methods
  - `Date.parse()`
  - `Date.UTC()`
  - `Date.now()` Return timestamp in millisecond

- Inherited Methods
  - `toLocaleString()` locale, includes AM or PM
  - `toString()` with time-zone information, 24-hour notation
  - `valueOf()` return the milliseconds representation of the date
    so that operators (such as less-than and greater-than) will work appropriately for date values.

- Date-Formatting Methods
  - `toDateString()` Displays the date’s day of the week, month, day of the month, and year in an implementation-specific format.
  - `toTimeString()` Displays the date’s hours, minutes, seconds, and time zone in an implementation-specific format.
  - `toLocaleDateString()` Displays the date’s day of the week, month, day of the month, and year in an implementation- and locale-specific format.
  - `toLocaleTimeString()` Displays the date’s hours, minutes, and seconds in an implementation-specific format.
  - `toUTCString()` Displays the complete UTC date in an implementation-specific format.

#### 5.2 The RegExp Type

- Regular expressions
  - `let expression = /pattern/flags;`

- Flags
  - `g` Indicates global mode, meaning the pattern will be applied to all of the string instead of stopping after the first match is found.
  - `i` Indicates case-insensitive mode, meaning the case of the pattern and the string are ignored when determining matches.
  - `m` Indicates multiline mode, meaning the pattern will continue looking for matches after reaching the end of one line of text.
  - `y` Indicates sticky mode, meaning the pattern will only look at the string contents beginning at lastIndex.
  - `u` Indicates Unicode mode is enabled.

- Metacharacters
  - `( [ { \ ^ $ | ) ] } ? * + .`

#### 5.3 Primitive Wrapper Type

#### 5.4 Singleton Built-in Objects

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


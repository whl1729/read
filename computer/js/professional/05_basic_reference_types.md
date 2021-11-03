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

- Two ways to define regular expressions
  - The literal form: `let pattern1 = /[bc]at/i`
  - The RegExp constructor: `let pattern2 = new RegExp("[bc]at", "i")`
    - Regular-expression literals should not be passed into the RegExp constructor.
    - All metacharacters must be double-escaped.
  - The literal form can't accept dynamic input, i.e. from variables, whereas the constructor can.
  - How to choose
    - For small regex, literals are definitely the way to go.
    - If you have a dynamic expression or a very long regex to maintain, RegExp is a nice option.

- RegExp Instance Properties
  - global
  - ignoreCase
  - unicode
  - sticky
  - lastIndex
  - multiline
  - source
  - flags

- RegExp Instance Methods
  - `exec` returns an array of information about the first match or null if no match was found.
    - `index` returns the location in the string where the pattern was matched.
    - `input` returns the string that the expression was run against.
  - `test` returns true if the pattern matches the argument and false if it does not.
  - `toLocaleString` and `toString` return the literal representation of the regular expression.

- How flag affects `exec`
  - With the global g flag set on the pattern,
    each call to exec() moves further into the string looking for matches.
  - With the sticky y flag set on the pattern,
    each call to exec() will search for a match in the string only at lastIndex.
    The sticky flag overrides the global flag.

- RegExp Constructor Properties
  - `input` or `$_`
  - `lastMatch` or `$&`
  - `lastParen` or `$+`
  - `leftContext` or $\`
  - `rightContext` or `$'`

#### 5.3 Primitive Wrapper Type

- A special behavior of primitive wrapper type
  - Every time a primitive value is read,
    an object of the corresponding primitive wrapper type is created behind the scenes,
    allowing access to any number of methods for manipulating the data.

  ```javascript
  let s1 = "some text"
  let s2 = s1.substring(2)

  // The above codes is equal to
  let s1 = new String("some text")
  let s2 = s1.substring(2)
  s1 = null
  ```

- The major difference between reference types and primitive wrapper types is the **lifetime** of the object.
  - When you instantiate a reference type using the new operator, it stays in memory until it goes out of scope,
  - whereas automatically created primitive wrapper objects exist for only one line of code before they are destroyed.

  ```javascript
  let s1 = "some text"
  s1.color = "red"
  console.log(s1.color)  // undefined
  ```

> 伍注：js的这个怪异行为看上去很挫，写代码时要小心。

- The Boolean Type
  - `valueOf` returns true or false
  - `toString` returns "true" or "false"
  - `typeof` returns "object"

- The Number Type
  - `valueOf` returns the primitive numeric value
  - `toString`
  - Format floating numbers as strings
    - `toFixed`
    - `toExponential`
    - `toPrecision`
  - `isInterger`
  - `isSafeInteger` returns true if the integer is between [-2^53 + 1, 2^53 - 1]

- The String Type
  - `valueOf`, `toLocaleString` and `toString` returns the object's primitive string value
  - `length`

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


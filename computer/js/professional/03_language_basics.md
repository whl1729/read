# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 3: Language Basics

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

#### 一级大纲

- Syntax
- Keywords and Reserved Words
- Variables
- Data Types
- Operators
- Statements
- Functions

#### 二级大纲

- Syntax
  - Case-Sensitivity
  - Identifiers
  - Comments
  - Strict Mode
  - Statements
- Keywords and Reserved Words
- Variables
  - The `var` Keyword
  - `let` Declarations
  - `const` Declarations
  - Declaration Styles and Best Practices
- Data Types
  - The typeof Operator
  - The Undefined Type
  - The Null Type
  - The Boolean Type
  - The Number Type
  - The String Type
  - The Symbol Type
  - The Object Type
- Operators
  - Unary Operators
  - Bitwise Operators
  - Boolean Operators
  - Multiplicative Operators
  - Exponentiation Operators
  - Additive Operators
  - Relational Operators
  - Equality Operators
  - Conditional Operator
  - Assignment Operators
  - Comma Operator
- Statements
  - The if Statement
  - The do-while Statement
  - The while Statement
  - The for Statement
  - The for-in Statement
  - The for-of Statement
  - Labeled Statements
  - The break and continue Statements
  - The with Statement
  - The switch Statement
- Functions

### Q3：作者想要解决什么问题

- Reviewing syntax
- Working with data types
- Working with flow-control statements
- Understanding functions

### Q4：这一章的关键词是什么

- Strict Mode
- Exponentiation Operators
- for-in
- for-of
- Temporal dead zone
- The window object
- Template literal
- Symbol.iterator
- Symbol.asyncIterator

### Q5：这一章的关键句是什么

#### 3.1 Syntax

- ECMAScript’s syntax borrows heavily from C and other C-like languages such as Java and Perl.

- Case-Sensitivity
  - The first concept to understand is that everything is case-sensitive.

- Identifiers
  - By convention, ECMAScript identifiers use camel case.

- Comments
  - ECMAScript uses C-style comments for both single–line and block comments.

  ```javascript
  // single line comment

  /* This is a multi-line
     comment */
  ```

- Strict Mode
  - ECMAScript 5 introduced the concept of strict mode.
  - Strict mode is a different parsing and execution model for JavaScript,
    where some of the erratic behavior of ECMAScript 3 is addressed and errors are thrown for unsafe activities.
  - Strict mode makes several changes to normal JavaScript semantics:
    - Eliminates some JavaScript silent errors by changing them to throw errors.
    - Fixes mistakes that make it difficult for JavaScript engines to perform optimizations:
      strict mode code can sometimes be made to run faster than identical code that's not strict mode.
    - Prohibits some syntax likely to be defined in future versions of ECMAScript.
  - To enable strict mode for an entire script, include the following at the top: `"use strict";`

- Statements
  - Even though a semicolon is not required at the end of statements, you should always include one.
    - Including semicolons helps prevent errors of omission.
    - Including semicolons also improves performance in certain situations
      because parsers try to correct syntax errors by inserting semicolons where they appear to belong.
  - It is a best practice to always use code blocks with control statements, even if there’s only one statement.

#### 3.2 Keywords and Reserved Words

- It’s best to avoid using both keywords and reserved words as both identifiers and property names
  to ensure compatibility with past and future ECMAScript editions.

#### 3.3 Variables

- The `var` Keyword
  - It is still possible to not only change the value stored in the variable but also change the type of value.
  - Using the var operator to define a variable makes it **local** to the function scope in which it was defined.
  - You would define a global variable if you omit the var/let/const operator.
  - var Declaration Hoisting: The interpreter pulls all variable declarations to the top of its scope.
    - You can use a variable before var declaration.
    - You can use redundant var declarations without penalty.

  ```javascript
  function test() {
    var message = "hi";  // local variable
  }

  function test2() {
    message = "hi";  // global variable
  }
  ```

- `let` vs `var`
  - let is block scoped, but var is function scoped.
  - let declarations does not allow for any redundant declarations within a block scope, while var does.
  - let declarations cannot be used in a way that assumes hoisting, while var does.
    - The segment of execution that occurs before the declaration is referred to as the "temporal dead zone".
  - when declaring variables using let in the global context, variables will not attach to the window object as they do with var.

- `const` Declarations
  - const behaves identically to that of let but with one important difference—
    it must be initialized with a value, and that value cannot be redefined after declaration.
  - The const declaration is only enforced with respect to the reference to the variable that it points to.
    If a const variable references an object, it does not violate the const constraints to modify properties inside that object.
  - if you were to declare a for loop variable that is not modified, const is allowed—
    precisely because a new variable is declared for each iteration.

  ```javascript
  for (const value of [1,2,3,4,5]) {
    console.log(value)
  }
  ```

- Declaration Styles and Best Practices
  - Don't Use var
  - Prefer const Over let

#### 3.4 Data Types

- There are six simple data types (also called primitive types) in ECMAScript:
  - Undefined
  - Null
  - Boolean
  - Number
  - String
  - Symbol

- There is also one complex data type called **Object**, which is an unordered list of name–value pairs.

##### 3.4.1 The typeof Operator

- Using the typeof operator on a value returns one of the following strings:
  - "undefined" if the value is undefined
  - "boolean" if the value is a Boolean
  - "string" if the value is a string
  - "number" if the value is a number
  - "object" if the value is an object (other than a function) or null
  - "function" if the value is a function
  - "symbol" if the value is a Symbol

##### 3.4.2 The Undefined type

- The typeof operator returns "undefined" when called on an uninitialized variable or undeclared variable.

- You should never explicitly set a variable to be undefined.
  - The literal undefined value is provided mainly for comparison and
    formalizing the difference between an empty object pointer (null) and an uninitialized variable.

- You should always initialize variables.
  - That way, when typeof returns "undefined",
    you’ll know that it’s because a given variable hasn’t been declared rather than was simply not initialized.

- The value undefined is falsy.

##### 3.4.3 The Null type

- Logically, a null value is an empty object pointer.

- When defining a variable that is meant to later hold an object,
  initialize the variable to null as opposed to anything else.
  - That way, you can explicitly check for the value null to determine if the variable has been filled with an object reference at a later time.

- Using the equality operator (==) between null and undefined always returns true.

  ```javascript
  console.log(null == undefined);  // true
  ```

- Any time an object is expected but is not available, null should be used in its place.
  - This helps to keep the paradigm of null as an empty object pointer and further differentiates it from undefined.

- The null type is falsy.

##### 3.4.4 The Boolean Type

- The Boolean literals true and false are case–sensitive,
  - So True and False are valid as identifiers but not as Boolean values.

- The `Boolean()` casting function can be called on any type of data and will always return a Boolean value.

  | Data type | Values converted to true | Values converted to false |
  | --------- | ------------------------ | ------------------------- |
  | Boolean   | true                     | false                     |
  | String    | Any nonempty string      | "" (empty string)         |
  | Number    | Any nonzero number(including infinity) | 0, NaN      |
  | Object    | Any object               | null                      |
  | Undefined | n/a                      | undefined                 |

##### 3.4.5 The Number Type

- ECMAScript uses the IEEE-754 format to represent both integers and floating-point values.

- Integer Values
  - If a number out of this range is detected in the octal literal,
    then the leading zero is ignored and the number is treated as a decimal.
  - Letters in the hexadecimal literal may be in uppercase or lowercase.

  ```javascript
  let octalNum = 079; // invalid octal - interpreted as 79
  ```

- Floating-Point Values
  - For very large or very small numbers, floating-point values can be represented using e-notation.
  - By default, ECMAScript converts any floating-point value with at least six zeros after the decimal point into e-notation.

  ```javascript
  let floatNum = .1;  // valid, but not recommended
  let floatNum2 = 0.0000001;  // 1e-7
  ```

- Range of Values
  - Number.MIN_VALUE = 5e-324
  - Number.MAX_VALUE = 1.7976931348623157e+308
  - Positive infinity: `Infinity`
  - Negative infinity: `-Infinity`
  - `isFinite()` returns true only if the argument is between the minimum and the maximum values

- NaN
  - Short for Not a Number
  - Used to indicate when an operation intended to return a number has failed.
  - Any operation involving NaN always returns NaN.
  - NaN is not equal to any value, including NaN.
  - `isNaN()` determines if the value is "not a number.".
    - Although typically not done, `isNaN()` can be applied to objects.
    - The `valueOf()` or `toString()` may be called.

- Number Conversions
  - `Number()`
  - `parseInt()`
  - `parseFloat()`

##### 3.4.6 The String Type

- Strings can be delineated by
  - either double quotes ("), single quotes ('), or backticks (\`).

- Immutability
  - Strings are immutable in ECMAScript,
    meaning that once they are created, their values cannot change.
  - Tochange the string held by a variable,
    the original string must be destroyed and the variable filled with another string containing a new value.

- Converting to a String
  - Two ways: `toString()` or `String()`
  - When used on a number value, `toString()` actually accepts a single argument:
    the radix in which to output the number.
  - The `String()` function follows these rules:
    - If the value has a toString() method, it is called (with no arguments) and the result is returned.
    - If the value is null, "null" is returned.
    - If the value is undefined, "undefined" is returned.

- Template Literals
  - Template literals are literals delimited with backticks (\`),
    allowing embedded expressions called substitutions.
  - Untagged template literals result in strings,
    which makes them useful for string interpolation (and multiline strings, since unescaped newlines are allowed).
  - Tagged template literals call a function (the tag function) with an array of any text segments from the literal
    followed by arguments with the values of any substitutions.
  - Use `String.raw` to create raw string.
  - The raw values are available as a property on each element in the string piece collection inside the tag function.

##### 3.4.7 The Symbol Type

- Basic Symbol Use

  ```javascript
  let sym = Symbol()
  let fooSymbol = Symbol('foo')
  ```

- Using the Global Symbol Registry

  ```javascript
  let fooGlobalSymbol = Symbol.for('foo')
  console.log(Symbol.keyFor(fooGlobalSymbol))  // foo
  ```

- Using Symbols as Properties

- Well-Known Symbols
  - Symbol.asyncIterator
  - Symbol.isConcatSpreadable
  - Symbol.iterator
  - Symbol.match
  - Symbol.replace
  - Symbol.search
  - Symbol.species
  - Symbol.split
  - Symbol.toPrimitive
  - Symbol.toStringTag
  - Symbol.unscopables

##### 3.4.8 The Object Type

- Each Object instance has the following properties and methods:
  - constructor
  - hasOwnProperty(propertyName)
  - isPrototypeof(object)
  - propertyIsEnumerable(propertyName)
  - toLocaleString()
  - valueoOf()

#### 3.5 Operators

- Unary Operators
  - `++, --, +, -`

- Bitwise Operators
  - Bitwise NOT: `~`
  - Bitwise AND: `&`
  - Bitwise OR: `|`
  - Bitwise XOR: `^`
  - Left Shift: `<<`
  - Signed Right Shift: `>>`
  - Unsigned Right Shift: `>>>`
    - The empty bits get filled with zeros regardless of the sign of the number.

- Boolean Operators
  - `!, &&, ||`
  - Logical AND/OR does not always return a Boolean value.
  - Short-circuited

- Multiplicative Operators
  - `*, /, %`

- Exponentiation Operator
  - `**, Math.pow()`

- Additive Operators
  - `+, -`

- Relational Operators
  - If one operand is a number,
    convert the other operand to a number and perform a numeric comparison.
  - If an operand is an object,
    call valueOf() and use its result to do comparison.
    If valueOf() is not available,
    call toString() and use its result to do comparison.
  - If an operand is a Boolean,
    convert it to a number and perform the comparison.
  - The result of any relational operation with NaN is false.

- Equality Opertors
  - Two sets of operators:
    - equal and not equal to perform conversion before comparison,
    - **identically equal** and not identically equal to perform comparison without conversion.
  - You should always use identically equal and not identically equal.

- Conditional Operator
  - `variable = boolean_expression ? true_value : false_value;`

- Assignment Operators
  - `-, *=, /=, %=, +=, -=, <<=, >>=, >>>=`

- Comma Operator
  - allows execution of more than one operation in a single statement
  - returns the value of last expression

#### 3.6 Statements

- The if Statement

- The do-while Statement

- The while Statement

- The for Statement

- The for-in Statement
  - Enumerate the non-symbol keyed properties of an object.

- The for-of Statement
  - Loop through elements in an iterable object.
  - Iterate in the order that the iterable produces values via its next() method.
  - Throw an error if the entity that it is attempting to iterate over does not support iteration.

- Labeled Statements

- The break and continue Statements

- The with Statement
  - The with statement sets the scope of the code within a particular object.

- The switch Statement
  - The switch statement works with all data types.
  - The case values need not be constants; they can be variables and even expressions.

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

#### Q8.1: 如何快速判断一个小数是否在IEEE 754标准下被精确表示

答：IEEE 754 能够表示的小数的通式为`sum(power(2, i))`，其中i为任意整数。
假设最低的幂为k，那么这个小数乘以`|k|`后就变成整数了。 由此不难得到一个判断方法：
将小数不断乘以2的若干次方，若最终能变成整数，则该小数能精确表示，否则不难。
这也意味着：每次运算时，小数的最后一位只能为5，若不为5则可以立即判断不能精确表示了。

#### Q8.2: Why is Number.MIN_VALUE 5e-324, and why is Number.MAX_VALUE 1.7976931348623157e+308

MIN_VALUE的取值与subnormal有关。MAX_VALUE的取值直接由最大底数乘以最大指数得到。

详见[Double-precision floating-point format][1]。

```text
0000 0000 0000 0001 ≙ +2−1022 × 2−52 = 2−1074 ≈ 4.9406564584124654 × 10−324 (Min. subnormal positive double)
000F FFFF FFFF FFFF ≙ +2−1022 × (1 − 2−52) ≈ 2.2250738585072009 × 10−308 (Max. subnormal double)
0010 0000 0000 0000 ≙ +2−1022 × 1 ≈ 2.2250738585072014 × 10−308 (Min. normal positive double)
7FEF FFFF FFFF FFFF ≙ +21023 × (1 + (1 − 2−52)) ≈ 1.7976931348623157 × 10308 (Max. Double)
```

#### Q8.3 Why does `isFinite(Number.MAX_VALUE + 1000)` still return true

IEEE 754 标准规定: 只有大于等于`1.7976931348623158e+308` 的数才会被 round 到 Infinity.
而 Number.MAX_VALUE 才是 `1.7976931348623157e+308`, 加上 1000 还远远不到 Infinity.

详见[为什么在js中Number.MAX_VALUE + 1不是Infinity？ - icymindx的回答 - 知乎][2]。

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系

  [1]: https://en.wikipedia.org/wiki/Double-precision_floating-point_format
  [2]: https://www.zhihu.com/question/24423421/answer/140269663

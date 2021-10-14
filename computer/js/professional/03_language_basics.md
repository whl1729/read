# 《Professional JavaScript for Web Developers》分析笔记

## Chapter 3: Language Basics

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

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

### Q3：作者想要解决什么问题？

- Reviewing syntax
- Working with data types
- Working with flow-control statements
- Understanding functions

### Q4：这一章的关键词是什么？

- Strict Mode
- Exponentiation Operators
- for-in
- for-of
- temporal dead zone"
- The window object

### Q5：这一章的关键句是什么？

#### 5.1 Syntax

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
  -  it is a best practice to always use code blocks with control statements, even if there’s only one statement.

#### 5.2 Keywords and Reserved Words

- It’s best to avoid using both keywords and reserved words as both identifiers and property names
  to ensure compatibility with past and future ECMAScript editions.

#### 5.3 Variables

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

#### 5.4 Data Types

- There are six simple data types (also called primitive types) in ECMAScript:
  - Undefined
  - Null
  - Boolean
  - Number
  - String
  - Symbol

- There is also one complex data type called **Object**, which is an unordered list of name–value pairs.

- Using the typeof operator on a value returns one of the following strings:
  - "undefined" if the value is undefined
  - "boolean" if the value is a Boolean
  - "string" if the value is a string
  - "number" if the value is a number
  - "object" if the value is an object (other than a function) or null
  - "function" if the value is a function
  - "symbol" if the value is a Symbol

- The Undefined type
  - The typeof operator returns "undefined" when called on an uninitialized variable or undeclared variable.
  - You should never explicitly set a variable to be undefined.
    The literal undefined value is provided mainly for comparison and
    formalizing the difference between an empty object pointer (null) and an uninitialized variable.
  - You should always initialize variables. That way, when typeof returns "undefined",
    you’ll know that it’s because a given variable hasn’t been declared rather than was simply not initialized.
  - The value undefined is falsy.

- The Null type
  - Logically, a null value is an empty object pointer.
  - When defining a variable that is meant to later hold an object, initialize the variable to null as opposed to anything else.
    That way, you can explicitly check for the value null to determine if the variable has been filled with an object reference at a later time.
  - Using the equality operator (==) between null and undefined always returns true.
  - Any time an object is expected but is not available, null should be used in its place.
    This helps to keep the paradigm of null as an empty object pointer and further differentiates it from undefined.
  - The null type is falsy.

  ```javascript
  console.log(null == undefined);  // true
  ```

- The Boolean Type
  - The Boolean literals true and false are case–sensitive,
    so True and False (and other mixings of uppercase and lowercase) are valid as identifiers but not as Boolean values.
  - The `Boolean()` casting function can be called on any type of data and will always return a Boolean value.

  | Data type | Values converted to true | Values converted to false |
  | --------- | ------------------------ | ------------------------- |
  | Boolean   | true                     | false                     |
  | String    | Any nonempty string      | "" (empty string)         |
  | Number    | Any nonzero number(including infinity) | 0, NaN      |
  | Object    | Any object               | null                      |
  | Undefined | n/a                      | undefined                 |

#### 5.5 Operators

#### 5.6 Statements

#### 5.7 Functions

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


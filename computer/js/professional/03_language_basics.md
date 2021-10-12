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

#### 5.4 Data Types

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


# 《Effective Python: 59 Specific Ways to Write Better Python》分析笔记

## Q1：这本书属于哪一类别的书

计算机/编程语言/Python

## Q2：这本书的内容是什么

介绍 Python 语言编程规范。

## Q3：这本书的大纲是什么

### 一级目录

- ch01 Pythonic Thinking
- ch02 Lists and Dictionaries
- ch03 Functions
- ch04 Comprehensions and Generators
- ch05 Classes and Interfaces
- ch06 Metaclasses and Attributes
- ch07 Concurrency and Parallelism
- ch08 Robustness and Performance
- ch09 Testing and Debugging
- ch10 Collaborations

## Q4：作者想要解决什么问题

## Q5：这本书的关键词是什么

## Q6：这本书的关键句是什么

### Item

- Item 2: Follow the PEP 8 Style Guide
- Item 20: Prefer Raising Exceptions to Returning None
- Item 40: Initialize Parent Classes with super
- Item 42: Prefer Public Attributes Over Private Ones
- Item 44: Use Plain Attributes Instead of Setter and Getter Methods

### ch01 Pythonic Thinking

#### Item 2: Follow the PEP 8 Style Guide

##### Whitespace

- Continuations of long expressions onto additional lines should be indented by **four extra spaces** from their normal indentation level.

- In a file, functions and classes should be separated by **two blank lines**.

##### Expressions and Statements

- Use inline negation (`if a is not b`) instead of negation of positive expressions (`if not a is b`).

> 伍注：前者可读性更好。

- Don’t check for empty containers or sequences (like [] or '' ) by comparing the length to zero (`if len(somelist) == 0`).
  - Use `if not somelist` and assume that empty values will implicitly evaluate to False .

> 伍注：后者可读性更好，也更简洁。

- The same thing goes for non-empty containers or sequences (like [1] or 'hi' ).
  - The statement `if somelist` is implicitly True for non-empty values.

- Avoid single-line `if` statements, `for` and `while` loops, and `except` compound statements.
  - Spread these over multiple lines for **clarity**.

- If you can’t fit an expression on one line, surround it with parentheses and add line breaks and indentation to make it easier to read.

- Prefer surrounding multiline expressions with parentheses over using the `\` line continuation character.

## Q7：作者是怎么论述的

## Q8：作者解决了什么问题

## Q9：我有哪些疑问

## Q10：这本书说得有道理吗？为什么

## Q11: 这本书讨论的知识的本质是什么

## Q12: 这本书讨论的知识的第一原则是什么

## Q13：这本书讨论的知识的结构是怎样的

## Q14：这本书讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

## Q15：有哪些相似的知识？它们之间的联系是什么

## Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

## Q17: 这本书对我有哪些用处/帮助/启示

## Q18: 我如何应用这本书的知识去解决问题

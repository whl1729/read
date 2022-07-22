# 《Go at Google: Language Design in the Service of Software Engineering》分析笔记

原文链接：[Go at Google: Language Design in the Service of Software Engineering][1]

## Q1: 这个文档属于哪一类别的文档？

计算机/编程语言/Go

## Q2：这个文档的内容是什么？

介绍 Go 语言设计的相关知识。

## Q3：这个文档的大纲是什么？

1. Abstract
2. Introduction
3. Go at Google
4. Pain points
5. Dependencies in C and C++
6. Enter Go
7. Dependencies in Go
8. Packages
9. Remote packages
10. Syntax
11. Naming
12. Semantics
13. Concurrency
14. Garbage collection
15. Composition not inheritance
16. Errors
17. Tools
18. Conclusion
19. Summary

## Q4：作者想要解决什么问题？

## Q5：这个文档的关键词是什么？

- CSP (Communicating sequential processes)

## Q6：这个文档的关键句是什么？

### 10. Syntax

- [Go 作者对 Syntax 重要性的认识][10]
  - Syntax is the user interface of a programming language.
  - Syntax determines the readability and hence clarity of the language.
  - Syntax is critical to tooling: if the language is hard to parse, automated tools are hard to write.

- Go was designed with clarity and tooling in mind, and has a clean syntax.
  - Its grammar is modest in size, with only 25 keywords
    (C99 has 37; C++11 has 84; the numbers continue to grow).
  - More important, the grammar is regular and therefore easy to parse.
  - Unlike C and Java and especially C++, Go can be parsed without type information or a symbol table;
    there is no type-specific context.
  - The grammar is easy to reason about and therefore tools are easy to write.

- Why doesn't Go support default function arguments
  - This was a deliberate simplification.
  - Experience tells us that defaulted arguments make it too easy to patch over API design flaws by adding more arguments,
    resulting in too many arguments with interactions that are difficult to disentangle or even understand.
  - The lack of default arguments requires more functions or methods to be defined,
    as one function cannot hold the entire interface, but that leads to a clearer API that is easier to understand.
  - Those functions all need separate names, too, which makes it clear which combinations exist,
    as well as encouraging more thought about naming, a critical aspect of clarity and readability.

> 伍注：不支持默认函数参数，是为了避免设计过于复杂的 API，并且迫使程序员通过函数命名提高可读性。

### 11. Naming

- Why does Go use the case of the initial letter of the identifier to determine the visibility
  - This was not an easy design decision.
  - We spent over a year struggling to define the notation to specify an identifier's visibility.
  - Once we settled on using the case of the name, we soon realized it had become one of the most important properties about the language.
  - The name is, after all, what clients of the package use;
  - putting the visibility in the name rather than its type means that it's always clear when looking at an identifier whether it is part of the public API.
  - After using Go for a while, it feels burdensome when going back to other languages that require looking up the declaration to discover this information.
  - The result is, again, clarity: the program source text expresses the programmer's meaning simply.

> 伍注：直接通过标记符的名字来确定接口的可见性，这样简单方便。

### 12. Semantics

- C-like
  - The semantics of Go statements is generally C-like.
  - It is a compiled, statically typed, procedural language with pointers and so on.

- Go makes many small changes to C semantics, mostly in the service of robustness.
  These include:
  - there is no pointer arithmetic
  - there are no implicit numeric conversions
  - array bounds are always checked
  - there are no type aliases (after type X int, X and int are distinct types not aliases)
  - `++` and `--` are statements not expressions
  - assignment is not an expression
  - it is legal (encouraged even) to take the address of a stack variable
  - and many more

- There are some much bigger changes too, stepping far from the traditional C, C++, and even Java models.
  These include linguistic support for:
  - concurrency
  - garbage collection
  - interface types
  - reflection
  - type switches

## Q7：作者是怎么论述的？

## Q8：作者解决了什么问题？

## Q9：我有哪些疑问？

### Q9.1: CSP 是什么？

### Q9.2: Go 的 interface 是如何实现的？

## Q10：这个文档说得有道理吗？为什么？

## Q11: 这个文档讨论的知识的本质是什么？

## Q12: 这个文档讨论的知识的第一原则是什么？

## Q13：这个文档讨论的知识的结构是怎样的？

## Q14：这个文档讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

## Q15：有哪些相似的知识？它们之间的联系是什么？

## Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

## Q17: 这个文档对我有哪些用处/帮助/启示？

## Q18: 我如何应用这个文档的知识去解决问题？

  [1]: https://go.dev/talks/2012/splash.article

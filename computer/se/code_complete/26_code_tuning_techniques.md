# 《Code Complete》分析笔记

## Chapter 26: Code-Tuning Techniques

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Logic
  - Stop testing when you know the answer
    - Short-circuit evaluation
  - Order tests by frequency
  - Substitute table lookups for complicated expressions
  - Use lazy evaluation
- Loops
  - Unswitching
  - Jamming
  - Unrolling
  - Minimizing the work inside loops
  - Sentinel values
  - Putting the busiest loop on the inside
  - Strength reduction
- Data Transformations
  - Use integers rather than floating-point numbers
  - Use the fewest array dimensions possible
  - Minimize array references
  - Use supplementary indexes
  - Use caching
- Expressions
  - Exploit algebraic identities
  - Use strength reduction
  - Initialize at compile time
  - Be wary of system routines
  - Use the correct type of constants
  - Precompute results
  - Eliminate common subexpressions
- Routines
  - Rewrite routines inline
- Recoding in a Low-Level Language
- The More Things Change, the More They Stay the Same

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Jamming
  - The result of combining two loops that operate on the same set of elements.
- Unrolling: 展开
- Strength Reduction
  - Replacing an expensive operation with a cheaper one

### Q5：这一章的关键句是什么？

#### 26.1 Logic

- Order Tests by Frequency
  - Arrange tests so that the one that’s fastest and most likely to be true is performed first.
  - This principle applies to case statements and to chains of if-then-elses.

#### 26.4 Expressions

- Strength reduction
  - Replace multiplication with addition.
  - Replace exponentiation with multiplication.
  - Replace trigonometric routines with their trigonometric identities.
  - Replace longlong integers with longs or ints
    (but watch for performance issues associated with using native-length vs. non-native-length integers)
  - Replace floating-point numbers with fixed-point numbers or integers.
  - Replace double-precision floating points with single-precision numbers.
  - Replace integer multiplication-by-two and division-by-two with shift operations.

#### 26.7 The More Things Change, the More They Stay the Same

- Performance issues have hardly changed at all.
  - Embedded systems
  - Real-time systems
  - Other systems with strict speed or space restrictions

- The need to measure the impact of each and every attempt at code tuning has been a constant.

- Code tuning invariably involves tradeoffs among complexity, readability, simplicity, and maintainability on the one hand and 
  a desire to improve performance on the other.

#### Checklist: Code-Tuning Techniques

- Improve Both Speed and Size
  - [ ] Substitute table lookups for complicated logic.
  - [ ] Jam loops.
  - [ ] Use integer instead of floating-point variables.
  - [ ] Initialize data at compile time.
  - [ ] Use constants of the correct type.
  - [ ] Precompute results.
  - [ ] Eliminate common subexpressions.
  - [ ] Translate key routines to a low-level language.

- Improve Speed Only
  - [ ] Stop testing when you know the answer.
  - [ ] Order tests in case statements and if-then-else chains by frequency.
  - [ ] Compare performance of similar logic structures.
  - [ ] Use lazy evaluation.
  - [ ] Unswitch loops that contain if tests.
  - [ ] Unroll loops.
  - [ ] Minimize work performed inside loops.
  - [ ] Use sentinels in search loops.
  - [ ] Put the busiest loop on the inside of nested loops.
  - [ ] Reduce the strength of operations performed inside loops.
  - [ ] Change multiple-dimension arrays to a single dimension.
  - [ ] Minimize array references.
  - [ ] Augment data types with indexes.
  - [ ] Cache frequently used values.
  - [ ] Exploit algebraic identities.
  - [ ] Reduce strength in logical and mathematical expressions.
  - [ ] Be wary of system routines.
  - [ ] Rewrite routines inline.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


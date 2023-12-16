# 《Code Complete》分析笔记

## Chapter 31: Laying Out Classes

### Q1：这一章的内容是什么

### Q2：这一章的大纲是什么

- Layout Fundamentals
- Layout Techniques
- Layout Styles
- Laying Out Control Structures
- Laying Out Individual Statements
- Laying Out Comments
- Laying Out Routines
- Laying Out Classes

### Q3：作者想要解决什么问题

### Q4：这一章的关键词是什么

### Q5：这一章的关键句是什么

#### Checklist: Layout

- General
  - [ ] Is formatting done primarily to illuminate the logical structure of the code?
  - [ ] Can the formatting scheme be used consistently?
  - [ ] Does the formatting scheme result in code that's easy to maintain?
  - [ ] Does the formatting scheme improve code readability?

- Control Structures
  - [ ] Does the code avoid doubly indented begin-end or {} pairs?
  - [ ] Are sequential blocks separated from each other with blank lines?
  - [ ] Are complicated expressions formatted for readability?
  - [ ] Are single-statement blocks formatted consistently?
  - [ ] Are case statements formatted in a way that’s consistent with the formatting of other control structures?
  - [ ] Have gotos been formatted in a way that makes their use obvious?

- Individual Statements
  - [ ] Is white space used to make logical expressions, array references, and routine arguments readable?
  - [ ] Do incomplete statements end the line in a way that’s obviously incorrect?
  - [ ] Are continuation lines indented the standard indentation amount?
  - [ ] Does each line contain at most one statement?
  - [ ] Is each statement written without side effects?
  - [ ] Is there at most one data declaration per line?

- Comments
  - [ ] Are the comments indented the same number of spaces as the code they comment?
  - [ ] Is the commenting style easy to maintain?

- Routines
  - [ ] Are the arguments to each routine formatted so that each argument is easy to read, modify, and comment?
  - [ ] Are blank lines used to separate parts of a routine?

- Classes, Files and Programs
  - [ ] Is there a one-to-one relationship between classes and files for most classes and files?
  - [ ] If a file does contain multiple classes,
        are all the routines in each class grouped together and is each class clearly identified?
  - [ ] Are routines within a file clearly separated with blank lines?
  - [ ] In lieu of a stronger organizing principle, are all routines in alphabetical sequence?

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系

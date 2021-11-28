# 《Code Complete》分析笔记

## Chapter 32: Self-Documenting Code

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- External Documentation
- Programming Style as Documentation
- To Comment or Not to Comment
- Keys to Effective Comments
- Commenting Techniques
- IEEE Standards

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

#### 32.0 Key Points

- The question of whether to comment is a legitimate one.
  - Done poorly, commenting is a waste of time and sometimes harmful.
  - Done well, commenting is worthwhile.
- The source code should contain most of the critical information about the program.
  - As long as the program is running, the source code is more likely than any other resource to be kept current,
    and it's useful to have important information bundled with the code.
- Good code is its own best documentation.
  - If the code is bad enough to require extensive comments,
    try first to improve the code so that it doesn't need extensive comments.
- Comments should say things about the code that the code can't say about itself—
  at the summary level or the intent level.
- Some commenting styles require a lot of tedious clerical work.
  - Develop a style that's easy to maintain.

#### Checklist: Good Commenting Technique

- General
  - [ ] Can someone pick up the code and immediately start to understand it?
  - [ ] Do comments explain the code's intent or summarize what the code does,
        rather than just repeating the code?
  - [ ] Is the Pseudocode Programming Process used to reduce commenting time?
  - [ ] Has tricky code been rewritten rather than commented?
  - [ ] Are comments up to date?
  - [ ] Are comments clear and correct?
  - [ ] Does the commenting style allow comments to be easily modified?

- Statements and Paragraphs
  - [ ] Does the code avoid endline comments?
  - [ ] Do comments focus on why rather than how?
  - [ ] Do comments prepare the reader for the code to follow?
  - [ ] Does every comment count? Have redundant, extraneous, and self-indulgent comments been removed or improved?
  - [ ] Are surprises documented?
  - [ ] Have abbreviations been avoided?
  - [ ] Is the distinction between major and minor comments clear?
  - [ ] Is code that works around an error or undocumented feature commented?

- Data Declarations
  - [ ] Are units on data declarations commented?
  - [ ] Are the ranges of values on numeric data commented?
  - [ ] Are coded meanings commented?
  - [ ] Are limitations on input data commented?
  - [ ] Are flags documented to the bit level?
  - [ ] Has each global variable been commented where it is declared?
  - [ ] Has each global variable been identified as such at each usage,
        by a naming convention, a comment, or both?
  - [ ] Are magic numbers replaced with named constants or variables rather than just documented?

- Control Structures
  - [ ] Is each control statement commented?
  - [ ] Are the ends of long or complex control structures commented or,
        when possible, simplified so that they don't need comments?

- Routines
  - [ ] Is the purpose of each routine commented?
  - [ ] Are other facts about each routine given in comments, when relevant,
        including input and output data, interface assumptions, limitations,
        error corrections, global effects, and sources of algorithms?

- Files, Classes, and Programs
  - [ ] Does the program have a short document, such as that described in the Book Paradigm,
        that gives an overall view of how the program is organized?
  - [ ] Is the purpose of each file described?
  - [ ] Are the author's name, e-mail address, and phone number in the listing?

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


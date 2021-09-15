# 《Unix Shells by Example》书籍分析笔记

## Chapter 4 The grep Family

### Q1：这一章的内容是什么？

介绍grep命令的基础知识，包括与正则表达式、选项的配合使用。

### Q2：这一章的大纲是什么？

- The grep Command
  - The Meaning of grep
  - How grep Works
  - Metacharacters
  - grep and Exit Status
- grep with Regular Expressions
- grep with Options
- grep with Pipes
- egrep
- GNU grep
- Recursive grep

### Q3：作者想要解决什么问题？

让读者掌握grep的基础知识、用法、不同grep变体之间的区别。

### Q4：这一章的关键词是什么？

- grep
- egrep
- fgrep
- rgrep
- GNU grep
- metacharacters

### Q5：这一章的关键句是什么？

#### 4.1.1 The Meaning of grep

- The name grep can be traced back to the ex editor.
- You would type at the ex prompt to search for a string: `:g/RE/p`
- It means "globally search for the regular expression (RE) and print out the line."

#### 4.1.2 How grep Works

- The grep command searches for a pattern of characters in a file or multiple files.
- If the pattern contains whitespace, it **must be quoted**.
- The pattern is either a quoted string or a single word, and all other words following it are **treated as filenames**.
- Grep sends its output to the screen and **does not change** or affect the input file in any way.

#### 4.1.3 Metacharacters

- `^` Beginning-of-line anchor
- `$` End-of-line anchor
- `.` Matches one character
- `*` Matches zero or more characters preceding the asterisk
- `[]` Matches one character in the set
- `[^]` Matches one character not in the set
- `\<` Beginning-of-word anchor
- `\>` End-of-word anchor
- `\(..\)` Tags matches characters.
  - Tags marked portion in a register to be remembered later as number 1. To reference later, use `\1` to repeat the pattern.
- `x\{m\}` Repetition of character x m times
- `x\{m,\}` Repetition of character x at least m times
- `x\{m,n\}` Repetition of character x between m and n times

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


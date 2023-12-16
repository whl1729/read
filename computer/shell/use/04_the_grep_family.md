# 《Unix Shells by Example》书籍分析笔记

## Chapter 4 The grep Family

### Q1：这一章的内容是什么

介绍grep命令的基础知识，包括与正则表达式、选项的配合使用。

### Q2：这一章的大纲是什么

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

### Q3：作者想要解决什么问题

让读者掌握grep的基础知识、用法、不同grep变体之间的区别。

### Q4：这一章的关键词是什么

- grep
- egrep
- fgrep
- rgrep
- GNU grep
- metacharacters

### Q5：这一章的关键句是什么

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

#### 4.1.3.1 New with egrep

- `+` Matches one or more of the characters preceding the + sign.
- `?` Matches zero or one of the preceding characters.
- `a|b` Matches either a or b.
- `()` Groups characters.

#### 4.1.3.2 New with GNU grep

In addition, GNU grep recognizes \b, \w, and \W, as well as a new class of POSIX metacharacters.

- `\w` Alphanumeric word character; `[a-zA-Z0-9_]`.
- `\W` Nonalphanumeric word character; `[^a-zA-Z0-9_]`.
- `\b` Word boundary.

#### 4.1.3.3 POSIX metacharacters

- `[:alnum:]` Alphanumeric characters
- `[:alpha:]` Alphabetic characters
- `[:cntrl:]` Control characters
- `[:digit:]` Numeric characters
- `[:graph:]` Nonblank characters (not spaces, control characters, etc.)
- `[:lower:]` Lowercase letters
- `[:print:]` Like [:graph:], but includes the space character
- `[:punct:]` Punctuation characters
- `[:space:]` All whitespace characters (newlines, spaces, tabs)
- `[:upper:]` Uppercase letters
- `[:xdigit:]` Allows digits in a hexadecimal number (0-9a-fA-F)

#### 4.1.4 grep's Options

- `-c` Displays a count of matching lines rather than displaying the lines that match.
- `-h` Does not display filenames.
- `-i` Ignores the case of letters in comparisons.
- `-l` Lists only the names of files with matching lines (once), separated by newline characters.
- `-n` Precedes each line by its relative line number in the file.
- `-v` Inverts the search to display only lines that do not match.
- `-w` Searches for the expression as a word, as if surrounded by `\<` and `\>`. This applies to grep only.

#### 4.12 GNU grep with Options

- `-A NUM, --after-context=NUM` Print NUM lines of trailing context after matching lines.
- `-B NUM, --before-context=NUM` Print # lines of leading context before matching lines.
- `-C NUM, -NUM, --context=NUM` Matches will be printed with NUM lines of leading and trailing context.
- `-a, --text, --binary-files=text` Processes binary files as text files.
- `-e PATTERN, --regexp=PATTERN` Use PATTERN literally as the pattern; useful to protect patterns beginning with -.
- `-n, --line-number` Prefix each line of output with the line number where the match occurred.
- `-v, --revert-match` Invert the sense of matching, to select nonmatch in lines.
- `-r` Read all files under each directory, recursively.

#### 4.1.5 grep and Exit Status

- grep returns an exit status to indicate whether it was able to locate the pattern or the file you were looking for.
  - If the pattern is found, grep returns an exit status of 0, indicating success;
  - If grep cannot find the pattern, it returns 1 as its exit status;
  - If the file cannot be found, grep returns an exit status of 2.

#### 4.7.1 Linux and GNU grep

- There are two versions of regular expression metacharacters: basic and extended.
  - The regular version of GNU grep (also `grep -G`) uses the basic set,
  - and egrep (or `grep -E`) uses the extended set.

- When regular grep use the extended set of metacharacters
  - Even without the -E option, regular grep, the default, can use the extended set of metacharacters,
    provided that the metacharacters are preceded with a backslash.
  - The extended set of metacharacters have no special meaning to regular grep, unless they are backslashed.

### Q6：作者是怎么论述的

### Q7：作者解决了什么问题

### Q8：我有哪些疑问

### Q9：这一章说得有道理吗？为什么

### Q10：如何拓展这一章

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象

### Q11：这一章和我有什么关系

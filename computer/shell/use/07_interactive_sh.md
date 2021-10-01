# 《Unix Shells by Example》分析笔记

## Chapter 7: The Interactive Bourne Shell

### Q1：这一章的内容是什么？

介绍在命令行中与Bourne Shell交互相关的基础知识。

### Q2：这一章的大纲是什么？

- The Environment
- The Command Line
- Shell Metacharacters (Wildcards)
- Filename Substitution
- Variables
- Quoting
- Command Substitution
- Functions
- Standard I/O and Redirection
- Pipes
- The here document

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- Command Substitution
- The here document

### Q5：这一章的关键句是什么？

#### 7.1 Introduction

- The processes before you see a shell prompt
  - `init` process starts to run
  - `init` gets instructions from `inittab`, or spawns a `getty` process
  - open up the terminal ports, and put a login prompt on your screen
  - The `/bin/login` is executed
  - The `/bin/sh` is executed
  - The `sh` executes `/etc/profile` and `~/.profile`
  - The `sh` awaits commands

#### 7.2 The Environment

- The environment of a process consists of 
  - variables, 
  - open files, 
  - the current working directory,
  - functions,
  - resource limits,
  - signals,
  - and so forth.

- The `/etc/profile` File
  - The /etc/profile file is a systemwide initialization file set up by the system administrator to perform tasks when the user logs on.
  - It is executed when the Bourne shell starts up.
  - It is available to all Bourne and Korn shell users on the system 
  - and normally performs such tasks as checking the mail spooler for new mail and displaying the message of the day from the /etc/motd file.

- The `.profile` File.
  - The .profile file is a user-defined initialization file executed once at login and found in your home directory.
  - It gives you the ability to customize and modify the shell environment.

- The Prompts
  - The primary prompt: PS1 = `$`
  - The secondary prompt: PS2 = `>`
  - The secondary prompt appears if you have partially typed a command and then pressed the carriage return.

- The PATH variable
  - is used by the Bourne shell to locate commands typed at the command line.

- The `hash` command
  - Controls the internal hash table used by the shell to improve efficiency in searching for commands.
  - Instead of searching the path each time a command is entered, the first time you type a command, the shell uses the search path to find the command, and then stores it in a table in the shell’s memory.
  - The next time you use the same command, the shell uses the hash table to find it.

- The dot command
  - Read and execute commands from the filename argument in the current shell context.
  - 伍注：bash提供了source命令，与dot命令作用相同。

#### 7.3 The Command Line

- The Exit Status
  - The exit status is a number between 0 and 255.
  - The shell status variable, ?, is set to the value of the exit status of the last command that was executed.

- Multiple Commands at the Command Line
  - A command line can consist of multiple commands.
  - Each command is separated by a **semicolon**, and the command line is terminated with a newline.
  - Commands may also be grouped so that all of the output is either piped to another command or redirected to a file.
  - Grouping Commands example: `(ls; pwd; date) > outputfile`

- Conditional Execution of Commands
  - With conditional execution, two command strings are separated by the special metacharacters,
    double ampersands (`&&`) and double vertical bars (`||`).
  - The command on the right will or will not be executed based on the exit condition of the command on the left.

- Commands in the Background
  - By placing an ampersand (`&`) at the end of the command line,
    the shell will return the shell prompt immediately and execute the command in the background concurrently. 

#### 7.4 Shell Metacharacters (Wildcards)

- `\` Literally interprets the following character
- `&` Processes in the background
- `;` Separates commands
- `$` Substitutes variables
- `?` Matches for a single character
- `[abc]` Matches for one character from a set of characters
- `[!abc]` Matches for one character not from the set of characters
- `[a–z]` Matches one character in the range from a to z
- `[!a–z]` Matches one character not in the range from a to z
- `*` Matches for zero or more characters
- `(cmds)` Executes commands in a subshell
- `{cmds}` Executes commands in current shell

> 伍注：shell取非集的符号是`!`，与grep/sed/awk使用的`^`不同。（经验证bash下面两者均可使用）

#### 7.5 Filename Substitution

- When evaluating the command line, the shell uses metacharacters to abbreviate filenames or pathnames that match a certain set of characters.
  - These metacharacters includes: `*, ?, [abc], [!abc], [a-z], [!a-z], \`

- The filename substitution metacharacters are expanded into an alphabetically listed set of filenames.

- The process of expanding the metacharacter into filenames is also called filename substitution, or globbing.

- If a metacharacter is used and there is no filename that matches it, the shell treats the metacharacter as a literal character.

#### 7.6 Variables

##### 7.6.1 Two Types of Variables

- There are two types of variables: local and environment.

- Local Variables
  - When assigning a value, there can be no whitespace surrounding the equal sign.
  - To set the variable to null, the equal sign is followed by a newline. 
  - A dollar sign is used in front of a variable to extract the value stored there.

- The Scope of Local Variables
  - A local variable is known only to the shell in which it was created.
  - It is **not passed** on to subshells.
  - The double dollar sign variable (`$$`) is a special variable containing the PID of the current shell.

- Setting Read-Only Variables
  - A read-only variable cannot be redefined or unset.

  ```shell
  $ name=Tom
  $ readonly name
  ```

- Environment Variables
  - Environment variables are available to the shell in which they are created and any subshells or processes spawned from that shell.
  - Some of the environment variables, such as HOME, LOGNAME, PATH, and SHELL, are set before you log on by the /bin/login program.
  - Normally, environment variables are defined and stored in the .profile file in the user’s home directory.
  - To set environment variables, the `export` command is used either after assigning a value or when the variable is set. 
  - Exported values are not propagated upward to the parent shell.

- Bourne Shell Environment Variables
  - `PATH` The search path for commands.
  - `HOME` Home directory; used by cd when no directory is specified.
  - `IFS` Internal field separators, normally space, tab, and newline.
  - `LOGNAME` The user’s login name.
  - `PWD` Present working directory.
  - `PS1` Primary prompt string, which is a dollar sign by default.
  - `PS2` Secondary prompt string, which is a right angle bracket by default.
  - `SHELL` When the shell is invoked, it scans the environment for this name.

##### 7.6.2 Set and Unset Variables

- Listing Set Variables
  - There are two built-in commands that print the value of a variable: `set` and `env`.
  - The `set` command prints all variables, local and global.
  - The `env` command prints just the global variables.

- Unsetting Variables
  - Both local and environment variables can be unset by using the unset command, unless the variables are set as read-only.

- Variable Expansion Modifiers
  - `${variable:-word}` If variable is set and is non-null, substitute its value; otherwise, substitute word.
  - `${variable:=word}` If variable is set or is non-null, substitute its value; otherwise, set it to word.
      The value of variable is substituted permanently. Positional parameters may not be assigned in this way.
  - `${variable:+word}` If parameter is set and is non-null, substitute word; otherwise, substitute nothing.
  - `${variable:?word}` If variable is set and is non-null, substitute its value; otherwise, print word and exit from the shell.
      If word is omitted, the message parameter null or not set is printed.

> 伍注：记忆技巧：
> -代表左值非空时**不要**替换为右值，
> +代表左值非空时**要**替换为右值（+代表加入、添加），
> =代表左值为空时**要**替换为右值。（安全起见，左值非空时不应赋值）
> ?好像没啥用，暂时不记。

##### 7.6.3 Speical Variables

- Bourne Shell Positional Parameters
  - `$0` References the name of the current shell script
  - `$1–$9` Denotes positional parameters 1 through 9
  - `$#` Evaluates to the number of positional parameters
  - `$*` Evaluates to all the positional parameters
  - `$@` Means the same as $*, except when double quoted
  - `"$*"` Evaluates to "$1 $2 $3"
  - `"$@"` Evaluates to "$1" "$2" "$3"

- Other Special Variables
  - `$` The PID of the shell
  - `-` The sh options currently set
  - `?` The exit value of last executed command
  - `!` The PID of the last job put in the background

#### 7.7 Quoting

- Quoting is used to protect special metacharacters from interpretation.

- There are three methods of quoting:
  - the backslash
  - single quotes
  - double quotes

- Special Metacharacters Requiring Quotes
  - `;` Command separator
  - `&` Background processing
  - `()` Command grouping; creates a subshell
  - `{}` Command grouping; does not create a subshell
  - `|` Pipe
  - `<` Input redirection
  - `>` Output redirection
  - `newline` Command termination
  - `space/tab` Word delimiter
  - `$` Variable substitution character
  - `*[]?` Shell metacharacters for filename expansion

- The Backslash
  - The backslash is used to quote (or escape) a single character from interpretation.
  - The backslash is not interpreted if placed in single quotes.
  - The backslash will protect the dollar sign ($), backquotes (` `), and the backslash from interpretation if enclosed in double quotes. 

- Single Quotes
  - Single quotes must be matched.
  - They protect all metacharacters from interpretation.
  - To print a single quote, it must be enclosed in double quotes or escaped with a backslash.

> 伍注：在bash里面，单引号里面无法再出现单引号（通过反斜杠转义也不行），只能在双引号中出现单引号。

#### 7.8 Command Substitution

- When a command is enclosed in backquotes, it will be executed and its output returned. This process is called **command substitution**.

- It is used when assigning the output of a command to a variable or when substituting the output of a command within a string.

- All three shells use backquotes to perform command substitution.

#### 7.9 An Introduction to Functions

- Defining Functions
  ```shell
  function_name () { commands ; commands; }
  ```

- Listing and Unsetting Functions
  - To list functions and their definitions, use the set command.
  - The function and its definition will appear in the output, along with the exported and local variables.
  - Functions and their definitions are unset with the unset command.

#### 7.10 Standard I/O and Redirection

- Redirection Operators
  - `<` Redirect input
  - `>` Redirect output
  - `>>` Append output
  - `2>` Redirect error
  - `1>&2` Redirect output to where error is going
  - `2>&1` Redirect error to where output is going
  - `3>&-` The output file descriptor 3 is closed.
  - `3<&-` The input file descriptor 3 is closed.

- Note that the order of redirections is significant. (From Bash's manpage)
  - `ls > dirlist 2>&1` directs both standard output and standard error to the file dirlist
  - `ls 2>&1 > dirlist` directs  only  the standard output to file dirlist,
    because the standard error was duplicated from the standard output before the standard output was redirected to dirlist.
  - For an more detailed explanation, see [Shell redirection i/o order][redirect].

  [redirect]: https://stackoverflow.com/questions/17975232/shell-redirection-i-o-order

- Redirecting Standard Output and Standard Error
  - Both the `&>file` and `>&file` are ok, but the first is preferred.

##### 7.10.1 The exec Command and Redirection

- `exec ls` Execute ls in place of the shell. When ls is finished, the shell in which it was started does not return.
- `exec < filea` Open filea for reading standard input.
- `exec > filex` Open filex for writing standard output.
- `exec 3< datfile` Open datfile as file descriptor 3 for reading input.
- `sort <&3` Sort datfile.
- `exec 4>newfile` Open newfile as file descriptor (fd) 4 for writing.
- `ls >&4` Output of ls is redirected to newfile.
- `exec 5<&4` Make fd 5 a copy of fd 4.
- `exec 3<&-` Close fd 3.

#### 7.12 The here document and Input

- The here document accepts inline text for a program expecting input until a user-defined terminator is reached.
  - It is often used in shell scripts for creating menus.

- The command receiving the input is appended with a `<<` symbol, followed by a user-defined word or symbol, and a newline.

- If the terminator is preceded by the `<<–` operator, leading tabs, and only tabs, may precede the final terminator.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

- Linux系统下的bash man手册也提供了shell的基础知识，可对比梳理一下。

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


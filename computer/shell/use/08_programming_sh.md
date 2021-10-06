# 《Unix Shells by Example》分析笔记

## Chapter 8: Programming the Bourne Shell

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Reading User Input
- Arithmetic
- Positional Parameters and Command-Line Arguments
- Conditional Constructs and Flow Control
- Looping Commands
- Functions
- Trapping Signals
- The Command Line
- Shell Invocation Options

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

#### 8.1 Introduction

- The First Line. 
  - The first line at the top left corner of the script will indicate the program that will be executing the lines in the script.
  - This line, known as the **shbang line**, is commonly written as `#!/bin/sh`.
  - The `#!` is called a magic number and is used by the kernel to identify the program that should be interpreting the lines in the script.
  - This line must be the top line of your script.

#### 8.2 Reading User Input

- The `read` Command
  - `read answer` Reads a line from standard input and assigns it to the variable answer.
  - `read first last` Reads a line from standard input to the first whitespace or newline,
    putting the first word typed into the variable first and the rest of the line into the variable last.

#### 8.3 Arithmetic

- Arithmetic is not built into the Bourne shell.
  - For simple integer arithmetic calculations, the UNIX `expr` command can be used.
  - For floating-point arithmetic, the awk or bc programs can be used.

- The performance of arithmetic in Borune shell
  - Because arithmetic was not built in, the performance of the shell is degraded when iterating through loops a number of times.
  - Each time a counter is incremented or decremented in a looping mechanism, it is necessary to fork another process to handle the arithmetic.

#### 8.4 Positional Parameters and Command-Line Arguments

- The `set` command and Positional Parameters
  - The set command with arguments resets the positional parameters. Once reset, the old parameter list is lost.
  - To unset all of the positional parameters, use `set --`.
  - `$0` is always the name of the script.

- The `$*` and `$@` differ only when enclosed in double quotes.
  - When `$*` is enclosed within double quotes, the parameter list becomes a single string.
  - When `$@` is enclosed within double quotes, each of the parameters is quoted; that is, each word is treated as a separate string.

- The quotes surrounding strings take no effect.
  - `set 'apple pie' pears peaches`
  - When $* is expanded, the quotes surrounding apple pie are stripped; apple and pie become two separate words.

#### 8.5 Conditional Constructs and Flow Control

##### 8.5.1 Testing Exit Status: The test Command

- The `test` Command
  - To evaluate an expression, the built-in `test` command is used.
  - This command is also linked to the **bracket symbol**.
  - Either the test command is used, or the expression can be enclosed in set of single brackets.
  - Shell metacharacters (wildcards) are not expanded by the test command.
  - The result of a command is tested, with zero status indicating success and nonzero status indicating failure. 

- String Test
  - `string1 = string2` String1 is equal to String2 (space surrounding = required)
  - `string1 != string2` String1 is not equal to String2 (space surrounding != required)
  - `string` String is not null
  - `–z string` Length of string is zero
  - `–n string` Length of string is nonzero

- Integer Test
  - `int1 -eq int2` Int1 is equal to int2
  - `int1 -ne int2` Int1 is not equal to int2
  - `int1 -gt int2` Int1 is greater than int2
  - `int1 -ge int2` Int1 is greater than or equal to int2
  - `int1 -lt int2` Int1 is less than int2
  - `int1 -le int2` Int1 is less than or equal to int2

- Logical Test
  - `expr1 -a expr2` Logical AND
  - `expr1 -o expr2` Logical OR
  - `! expr` Logical NOT

- File Test
  - `-b filename` Block special file
  - `-c filename` Character special file
  - `-d filename` Directory existence
  - `-f filename` Regular file existence and not a directory
  - `-g filename` Set-group-ID is set
  - `-k filename` Sticky bit is set
  - `-p filename` File is a named pipe
  - `-r filename` File is readable
  - `-s filename` File is nonzero size
  - `-u filename` Set-user-ID bit is set
  - `-w filename` File is writable
  - `-x filename` File is executable

##### 8.5.2 The if Command

- The command or UNIX utility following the if construct is executed and its exit status is returned. 

- If the exit status is zero, the command succeeded and the statement(s) after the then keyword are executed.

- It is important that you know the exit status of the commands being tested.

- Indenting the nested ifs
  - When if statements are nested, the fi statement always goes with the nearest if statement.
  - Indenting the nested ifs makes it easier to see which if statement goes with which fi statement.

##### 8.5.8 The null Command

- The null command, represented by a colon(:), is a built-in, do-nothing command that returns an exit status of 0.

- It is used as a placeholder after an if command when you have nothing to say,
  but need a command or the program will produce an error message because it requires something after the then statement.

- Often the null command is used as an argument to a looping command to make the loop a forever loop.

##### 8.5.9 The case Command

- How the `case` command works
  - The value of the case variable is matched against value1, value2, and so forth, until a match is found.
  - When a value matches the case variable, the commands following the value are executed until the double semicolons are reached.
    Then execution starts after the word esac.
  - If the case variable is not matched, the program executes the commands after the `*)`, the default value, 
    until `;;` or `esac` is reached.

- The case values allow the use of shell wildcards and the vertical bar (pipe symbol) for ORing two values.

```shell
case variable in
  value1)
    command(s)
    ;;
  value2)
    command(s)
    ;;
  *)
    command(s)
    ;;
esac
```

##### 8.5.10 Creating Menus with the here document and case Command

- Creating Menus
  - The here document and case command are often used together.
  - The here document is used to create a menu of choices that will be displayed to the screen.
  - The user will be asked to select one of the menu items,
    and the case command will test against the set of choices to execute the appropriate command.

#### 8.6 Looping Commands

- The Bourne shell has three types of loops: `for`, `while`, and `until`.

##### 8.6.1 The for Command

- The for Command Format
  ```shell
  for variable in word_list
  do
    command(s)
  done
  ```

- If the for loop is not provided with a wordlist, it iterates through the positional parameters. 
  This is the same as for `file in $*`.

##### 8.6.3 The while Command

- The while Command Format
  ```shell
  while command
  do
    command(s)
  done
  ```

- The while command evaluates the command immediately following it and,
  if its **exit status is 0**, the commands in the body of the loop (commands between do and done) are executed.

##### 8.6.4 The until Command

- The until Command Format
  ```shell
  until command
  do
    command(s)
  done
  ```

- How the until Command works
  - Executes the loop statements only if the command after until fails; that is,
    if the command returns an exit status of nonzero.
  - When the done keyword is reached,
    control is returned to the top of the loop and the until command checks the exit status of the command again.
  - Until the exit status of the command being evaluated by until becomes 0, the loop continues.
    When the exit status reaches 0, the loop exits, and program execution starts after the done keyword.

##### 8.6.5 Looping Control Commands

- The shift Command
  - `shift [n]` Shifts the parameter list to the left a specified number of times.
  - The shift command without an argument shifts the parameter list once to the left.
  - Once the list is shifted, the parameter is removed permanently.
  - Often, the shift command is used in a while loop when iterating through a list of positional parameters.

- The break Command
  - The built-in break command is used to force immediate exit from a loop, but not from a program.
  - The break command causes an exit from the innermost loop, so if you have nested loops,
    the break command takes a number as an argument(`break [n]`), allowing you to break out of a specific outer loop.
  - If you are nested in three loops,
    the outermost loop is loop number 3, the next nested loop is loop number 2, and the innermost nested loop is loop number 1.

- The continue Command
  - The continue command returns control to the top of the loop if some condition becomes true.
  - If nested within a number of loops, the continue command returns control to the innermost loop.
  - If a number is given as its argument(`continue [n]`), control can then be started at the top of any loop.
  - If you are nested in three loops,
    the outermost loop is loop number 3, the next nested loop is loop number 2, and the innermost nested loop is loop number 1.

> 伍注：shell 的break/continue语句可以带一个参数，以控制跳出第几层循环。这样虽然方便，但可读性可能不好，感觉要慎用。

##### 8.6.7 I/O Redirection and Subshells

- Input can be piped or redirected to a loop from a file.
- Output can also be piped to another command(s) or redirected to a file from a loop.
- The shell starts a subshell to handle I/O redirection and pipes.
- Any variables defined within the loop will not be known to the rest of the script when the loop terminates.

##### 8.6.8 Running Loops in the Background

- Loops can be executed to run in the background. The program can continue without waiting for the loop to finish processing.

##### 8.6.9 The exec Command and Loops

- The exec command can be used to open or close standard input or output without creating a subshell.
  - Therefore, when starting a loop, any variables created within the body of the loop will remain when the loop completes.
  - When using redirection in loops, any variables created within the loop are lost.

- The exec command is often used to open files for reading and writing, either by name or by file descriptor number.

##### 8.6.10 IFS and Loops

- The shell’s internal field separator (IFS) evaluates to spaces, tabs, and the newline character.

- `IFS` is used as a word (token) separator for commands that parse lists of words, such as read, set, and for.

- `IFS` can be reset by the user if a different separator will be used in a list.

- Before changing its value, it is a good idea to save the original value of the IFS in another variable.
  Then it is easy to return to its default value, if needed.

#### 8.7 Functions

##### 8.7.0 Important Rules about using Function

- The Bourne shell determines whether you are using a built-in command, a function, or an executable program found on the disk.
  - It looks for built-in commands first, then functions, and last, executables.

- A function must be defined before it is used.

- The function runs in the current environment
  - it shares variables with the script that invoked it, and lets you pass arguments by assigning them as positional parameters.
  - If you use the exit command in a function, you exit the entire script.
  - If either the input or output of the function is redirected or the function is enclosed within backquotes (command substitution),
    - a subshell is created and the function and its variables and present working directory are known only within the subshell.
    - When the function exits, any variables set there will be lost,
    - and if you have changed directories, you will revert to the directory you were in before invoking the function.
    - If you exit the function, you return to where the script left off when the function was invoked.

- The `return` statement returns the exit status of the last command executed within the function or the value of the argument given.

- The `set` command lists functions and definitions.

- Trap vs Function
  - Traps, like variables, are global within functions.
  - They are shared by both the script and the functions invoked in the script.
  - If a trap is defined in a function, it is also shared by the script. This could have unwanted side effects.

- The `dot` Command
  - Functions exist only in the shell where they are defined; they cannot be exported to subshells.
  - The dot command can be used to execute functions stored in files.
  - If functions are stored in another file, they can be loaded into the current script with the dot command.

##### 8.7.1 Unsetting Functions

- To remove a function from memory, the unset command is used.

##### 8.7.2 Function Arguments and the Return Value

- Function Arguments and Variables
  - Because the function is executed within the current shell, the variables will be known to both the function and the shell.
  - Any changes made to your environment in the function will also be made to the shell.
  - Arguments can be passed to functions by using positional parameters.
  - The positional parameters are private to the function;
    that is, arguments to the function will not affect any positional parameters used outside the function.

> 伍注：Bourne Shell 函数中定义的变量作用域是全局的，在函数外也能访问，要注意这个坑。

- Function Return Value
  - The return command can be used to exit the function and return control to the program at the place where the function was invoked.
  - If you use exit anywhere in your script, including within a function, the script terminates.
  - The return value of a function is really just the value of the exit status of the last command in the script,
    unless you give a specific argument to the return command.
  - If a value is assigned to the return command, that value is stored in the ? variable and can hold an integer value between 0 and 255.
  - Because the return command is limited to returning only an integer between 0 and 255,
    you can use **command substitution** to capture the output of a function.
    Place the entire function in backquotes and assign the output to a variable just as you would if getting the output of a UNIX command.

> 伍注：Bourne Shell 的函数返回值只能为0~255之间的整数，要返回字符串或其他范围的数字，可以使用「命令替换」的方式。

##### 8.7.3 Functions and the dot Command

- Storing Functions
  - Functions are often defined in the .profile file, so that when you log in, they will be defined.
  - Functions cannot be exported, but they can be stored in a file.
  - When you need the function, the dot command is used with the name of the file to activate the definitions of the functions within it.

#### 8.8 Trapping Signals

- The trap Command
  - `trap 'command; command' signal-number`
  - Allows you to control the way a program behaves when it receives a signal.
  - Tells the shell to terminate the command currently in execution upon the receipt of a signal.

- Command string
  - If the trap command is followed by commands within quotes, the command string will be executed upon receipt of a specified signal.
  - The shell reads the command string twice, once when the trap is set, and again when the signal arrives.
  - If the command string is surrounded by double quotes,
    all variable and command substitution will be performed when the trap is set the first time.
  - If single quotes enclose the command string,
    variable and command substitution do not take place until the signal is detected and the trap is executed.

- Use the command `kill -l` to get a list of all signals.

##### 8.8.1 Resetting Signals

- To reset a signal to its default behavior, the trap command is followed by the signal name or number.
  - eg: `trap 2`

##### 8.8.2 Ignoring Signals

- If the trap command is followed by a pair of empty quotes, the signals listed will be ignored by the process.
  - eg: `trap "" 1 2`

##### 8.8.4 Traps in Functions

- The trap is global to the script.
  - If you use a trap to handle a signal in a function, it will affect the entire script, once the function is called.

##### 8.8.5 Debugging

- Debugging Options
  - `sh -x scriptname` Echo option Displays each line of script after variable substitutions and before execution
  - `sh -v scriptname` Verbose option Displays each line of script before execution, just as you typed it
  - `sh -n scriptname` Noexec option Interprets but does not execute commands
  - `set -x` Turns on echo Traces execution in a script
  - `set +x` Turns off echo Turns off tracing

#### 8.9 The Command Line

##### 8.9.1 Processing Command-Line Options with getopts.

- If you are writing scripts that require a number of command-line options, positional parameters are not always the most efficient.

- If there is a **colon** after option, it means that the option requires a named argument.
  - eg: `getopts xyn: name` means the option `-n` requires a named argument that will be stored in `name`.
  - If an illegal argument is given, the named argument is assigned a **question mark**.

- `OPTIND`
  - The index of the next argument to be processed by the getopts builtin command.
  - Initialized to 1.

- `OPTARG`
  - The value of the last option argument processed by the getopts builtin command.

##### 8.9.2 The eval Command and Parsing the Command Line

- The eval command
  - Evaluates a command line, performs all shell substitutions, and then executes the command line.
  - Essentially, it parses the command line twice.
  - The eval command is used when normal parsing of the command line is not enough.

#### 8.10 Shell Invocation Options

- Shell Invocation options
  - `-i` Shell is in the interactive mode. QUIT and INTERRUPT are ignored.
  - `-s` Commands are read from standard input and output is sent to standard error.
  - `-c string` Commands are read from string.

##### 8.10.1 The set Command and Options

- The `set` Command 
  - Can be used to turn shell options on and off, as well as for handling command-line arguments.
  - To turn an option on, the dash (-) is prepended to the option;
  - To turn an option off, the plus sign (+) is prepended to the option.

- The `set` Command Options
  - `-a` Marks variables that have been modified or exported
  - `-e` Exits the program if a command returns a nonzero status
  - `-f` Disables globbing (filename expansion)
  - `-h` Locates and remembers function commands as functions when they are defined, not just when they are executed
  - `-k` Places all keyword arguments in the environment for a command, not just those that precede the command name
  - `-n` Reads commands but does not execute them; used for debugging
  - `-t` Exits after reading and executing one command
  - `-u` Treats unset variables as an error when performing substitution
  - `-v` Prints shell input lines as they are read; used for debugging
  - `-x` Prints commands and their arguments as they are being executed; used for debugging
  - `--` Does not change any of the flags

##### 8.10.2 Shell Built-In Commands

  - `:` Do-nothing command; returns exit status 0
  - `. file` The dot command reads and executes command from file
  - `break [n]` See “The break Command” on page 361
  - `cd` Change directory
  - `continue [n]`
  - `echo [ args ]` Echo arguments
  - `eval command` Shell scans the command line twice before execution
  - `exec command` Runs command in place of this shell
  - `exit [ n ]` Exit the shell with status n
  - `export [ var ]` Make var known to subshells
  - `hash` Controls the internal hash table for quicker searches for commands
  - `kill [ –signal process ]` Sends the signal to the PID number or job number of the process
  - `getopts` Used in shell scripts to parse command line and check for legal options
  - `login [ username ]` Sign onto the system
  - `newgrp [ arg ]` Logs a user into a new group by changing the real group and effective group ID
  - `pwd` Print present working directory
  - `read [ var ]` Read line from standard input into variable var
  - `readonly [ var ]` Make variable var read-only; cannot be reset
  - `return [ n ]` Return from a function where n is the exit value given to the return
  - `set` See section 8.10.1.
  - `shift [ n ]` Shift positional parameters to the left n times
  - `stop pid` Halt execution of the process number PID
  - `suspend` Stops execution of the current shell (but not if a login shell)
  - `times` Print accumulated user and system times for processes run from this shell
  - `trap [ arg ] [ n ]` When shell receives signal n ( 0, 1, 2, or 15 ), execute arg
  - `type [ command ]` Prints the type of command; for example, pwd has a built-in shell
  - `umask [ octal digits ]` User file creation mode mask for owner, group, and others
  - `unset [ name ]` Unset value of variable or function
  - `wait [ pid#n ]` Wait for background process with PID number n and report termination status
  - `ulimit [ options size ]` Set maximum limits on processes
  - `umask [ mask ]` Without argument, print out file creation mask for permissions
  - `wait [ pid#n ]` Wait for background process with PID number n and report termination status

#### 8.11 LAB 8: Bourne Shell -- Getting Started

- How do you know what shell you are using?
  ```shell
  echo $0
  echo $SHELL
  ps -p "$$"
  ```

- List three-character files where all letters are uppercase.
  - What characters `[A-Z]` matches depends on your locale. (伍注：我的Ubuntu下`[A-Z]`会匹配到小写字母)
  - `[A-Z]` doesn't mean upper case. It means letters from A to Z, which may include lower-case letters.
  - Usually you should use [[:upper:]] instead. (This works in Bash even without extglob.)

  ```shell
  ls [[:upper:]][[:upper:]][[:upper:]]
  ```

- Remove two-character files starting with a or A.
  ```shell
  rm [aA]?
  ```

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


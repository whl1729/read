# 《Go 语言项目开发实战》分析笔记

## 第16章 代码检查：如何进行静态代码检查？

### Q1：这一章的内容属于哪一类别？

计算机/软件工程

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- 为什么选择 golangci-lint 做静态代码检查？
- golangci-lint 提供了哪些命令和选项？
  - run 命令
  - cache 命令
  - completion 命令
  - config 命令
  - linters 命令
- golangci-lint 配置
- 如何使用 golangci-lint 进行静态代码检查？
- golangci-lint 使用技巧
  - 技巧1：第一次修改，可以按目录修改。
  - 技巧2：按文件修改，减少文件切换次数，提高修改效率。
  - 技巧3：把 linters-setting.lll.line-length 设置得大一些。
  - 技巧4：尽可能多地使用 golangci-lint 提供的 linter。
  - 技巧5：每次修改代码后，都要执行 golang-ci。
  - 技巧6：建议在根目录下放一个通用的 golangci-lint 配置文件。

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### golangci-lint 提供了哪些命令和选项？

- cache 命令
  - `golangci-lint cache clean` 当我们觉得 cache 的内容异常，或者 cache 占用空间过大时，
    可以用这条命令来清除 cache。
  - `golangci-lint cache status` 用来打印 cache 的状态，比如存放目录和大小。

- completion 命令
  - 包含 4 个子命令 bash、fish、powershell 和 zsh，分别用来输出对应 shell 的自动补全脚本。
  - 配置 bash 自动补全的示例

  ```bash
  golangci-lint completion bash > ~/.golangci-lint.bash
  echo "source '$HOME/.golangci-lint.bash'" >> ~/.bashrc
  source ~/.bashrc
  ```

- config 命令
  - `golangci-lint config path` 打印 golangci-lint 当前使用的配置文件路径

- linters 命令
  - `golangci-lint linters` 打印 golangci-lint 所支持的 linter

#### golangci-lint 配置

- golangci-lint 支持两种配置方式，分别是命令行选项和配置文件。
  - 如果 bool/string/int 的选项同时在命令行选项和配置文件中被指定，命令行的选项就会覆盖配置文件中的选项。
  - 如果是 slice 类型的选项，则命令行和配置中的配置会进行合并。

- `golangci-lint -h`
  - 查看 golangci-lint run 支持的命令行选项

- [golangci-lint configuration][1]

- [建议的 golangci.yaml 配置][2]

#### 如何使用 golangci-lint 进行静态代码检查？

- 5 种常见的 golangci-lint 使用方法
  - 如果想递归地检查一个目录，需要在目录后面追加`/...`，见方法2.
  - 你可以传入参数 `-E/--enable` 来使某个 linter 可用，见方法4.
  - 你也可以使用 `-D/--disable` 参数来使某个 linter 不可用。见方法5.
  - golangci-lint 寻找配置文件的方法
    - 默认情况下，golangci-lint 会从当前目录一层层往上寻找特定名字的配置文件直到根目录
    - 这些配置文件的名字可以是：.golangci.yaml、.golangci.toml、.golangci.json
    - 如果找到，就以找到的配置文件作为本次运行的配置文件
    - 为了防止读取到未知的配置文件，可以用 `--no-config` 参数使 golangci-lint 不读取任何配置文件。

  ```bash
  # 1. 对当前目录及子目录下的所有 Go 文件进行静态代码检查
  # 等价于：golangci-lint run ./...
  golangci-lint run

  # 2. 对指定的 Go 文件或者指定目录下的 Go 文件进行静态代码检查
  # 注意：这里不会检查 dir1 下面子目录的 Go 文件，除非改为 dir1/...
  golangci-lint run dir1 dir2/... dir3/file1.go

  # 3. 根据指定配置文件，进行静态代码检查
  golangci-lint run -c .golangci.yaml ./...

  # 4. 运行指定的 linter，比如以下仅仅启用了 errcheck linter
  golangci-lint run --no-config --disable-all -E errcheck ./...

  # 5. 如果我们想禁用某些 linter，可以使用-D选项
  golangci-lint run --no-config -D godot,errcheck
  ```

- 减少误报的三种方法
  - 排除某些要检查的错误
    - 在命令行中添加 `-e` 参数，或者在配置文件的 `issues.exclude` 部分设置要排除的检查错误。
    - 使用 `issues.exclude-rules` 来配置哪些文件忽略哪些 linter。
  - 排除某些要检查的目录或文件
    - 通过 `run.skip-dirs`、`run.skip-files` 或者 `issues.exclude-rules` 配置项，
      来忽略指定目录下的所有 Go 文件，或者指定的 Go 文件。
  - 排除某些要检查的代码行
    - 通过在 Go 源码文件中添加 `//nolint` 注释，来忽略指定的代码行。

- 使用 nolint
  - 首先，如果启用了 nolint，你就需要在 `//nolint` 后面添加 nolint 的原因 `// xxxx`。
  - 其次，你使用的应该是 `//nolint` 而不是 `// nolint`。
    因为根据 Go 的规范，需要程序读取的注释 // 后面不应该有空格。
  - 最后，如果要忽略所有 linter，可以用 `//nolint`；
    如果要忽略某个指定的 linter，可以用 `//nolint:<linter1>,<linter2>`。

    ```go
    // 忽略某一行所有 linter 的检查
    var bad_name int //nolint

    // 忽略某一行指定 linter 的检查，可以指定多个 linter，用逗号 , 隔开。
    var bad_name int //nolint:golint,unused

    // 忽略某个代码块的检查。
    //nolint
    func allIssuesInThisFunctionAreExcluded() *string { // ...}

    // 忽略某个文件的指定 linter 检查。
    // 在 package xx 上面一行添加//nolint注释。
    //nolint:unparam
    package pkg...
    ```

#### golangci-lint 使用技巧

- 技巧1：第一次修改，可以按目录修改。
  - 为了减轻修改的压力，可以按目录检查代码并修改。
  - 如果错误太多，一时半会儿改不完，想以后慢慢修改或者干脆不修复存量的 issues，
    那么你可以使用 golangci-lint 的 `--new-from-rev` 选项，只检查新增的 code，例如：

  ```bash
  golangci-lint run --new-from-rev=HEAD~1
  ```

- 技巧2：按文件修改，减少文件切换次数，提高修改效率。
  - 可以通过 grep 过滤出某个文件的检查失败项

- 技巧3：把 linters-setting.lll.line-length 设置得大一些。
  - 在 Go 项目开发中，为了易于阅读代码，通常会将变量名 / 函数 / 常量等命名得有意义
  - 这样很可能导致每行的代码长度过长，很容易超过lll linter 设置的默认最大长度 80
  - 这里建议将linters-setting.lll.line-length设置为 120/240。

- 技巧4：尽可能多地使用 golangci-lint 提供的 linter。
  - 每个 linter 都有两个属性：
    - fast：true/false，如果为 true，说明该 linter 可以缓存类型信息，支持快速检查。
      因为第一次缓存了这些信息，所以后续的运行会非常快。
    - auto-fix：true/false，如果为 true 说明该 linter 支持自动修复发现的错误；
      如果为 false 说明不支持自动修复。

- 技巧5：每次修改代码后，都要执行 golang-ci。

- 技巧6：建议在根目录下放一个通用的 golangci-lint 配置文件。
  - 可以让你不用为每一个项目都配置 golangci-lint。
  - 当你需要为某个项目单独配置 golangci-lint 时，只需在该项目根目录下增加一个项目级别的 golangci-lint 配置文件即可。

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

  [1]: https://golangci-lint.run/usage/configuration/
  [2]: basic_golangci.yaml

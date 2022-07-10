# 《Go 语言项目开发实战》分析笔记

## 第14章 项目管理：如何编写高质量的 Makefile？

### Q1：这一章的内容属于哪一类别？

计算机/软件工程

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- 熟练掌握 Makefile 语法
- 规划 Makefile 要实现的功能
- 设计合理的 Makefile 结构
- 掌握 Makefile 编写技巧
  - 技巧1：善用通配符和自动变量
  - 技巧2：善用函数
  - 技巧3：依赖需要用到的工具
  - 技巧4：把常用功能放在主 Makefile 中，不常用的功能放在分类 Makefile 中
  - 技巧5：编写可扩展的 Makefile
  - 技巧6：将所有输出放在一个目录下，方便清理和查找
  - 技巧7：使用带层级的命令方式
  - 技巧8：做好目标划分
  - 技巧9：设置 OPTIONS
  - 技巧10：定义环境变量
  - 技巧11：自己调用自己
- 总结

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 熟练掌握 Makefile 语法

- 建议重点掌握的语法
  - Makefile 规则语法
  - 伪目标
  - 变量赋值
  - 条件语句
  - Makefile 常用函数

#### 规划 Makefile 要实现的功能

- Go 项目的 Makefile 应该实现以下功能
  - 格式化代码
  - 静态代码检查
  - 单元测试
  - 代码构建
  - 软件部署
    - 如果通过 docker 部署，还需要有 docker 镜像打包功能。
    - 因为 Go 是跨平台的语言，所以构建和 docker 打包命令，还要能够支持不同的 CPU 架构和平台。
  - 文件清理
  - 选项
    - 为了能够更好地控制 Makefile 命令的行为，还需要支持 Options。
  - 帮助
    - 为了方便查看 Makefile 集成了哪些功能，我们需要支持 help 命令。help 命令最好通过解析 Makefile 文件来输出集成的功能

- IAM 项目 Makefile 所集成的功能

  ```bash
  $ make help

  Usage: make <TARGETS> <OPTIONS> ...

  Targets:
    # 代码生成类命令
    gen                Generate all necessary files, such as error code files.

    # 格式化类命令
    format             Gofmt (reformat) package sources (exclude vendor dir if existed).

    # 静态代码检查
    lint               Check syntax and styling of go sources.

    # 测试类命令
    test               Run unit test.
    cover              Run unit test and get test coverage.

    # 构建类命令
    build              Build source code for host platform.
    build.multiarch    Build source code for multiple platforms. See option PLATFORMS.

    # Docker镜像打包类命令
    image              Build docker images for host arch.
    image.multiarch    Build docker images for multiple platforms. See option PLATFORMS.
    push               Build docker images for host arch and push images to registry.
    push.multiarch     Build docker images for multiple platforms and push images to registry.

    # 部署类命令
    deploy             Deploy updated components to development env.

    # 清理类命令
    clean              Remove all files that are created by building.

    # 其他命令，不同项目会有区别
    release            Release iam
    verify-copyright   Verify the boilerplate headers for all files.
    ca                 Generate CA files for all iam components.
    install            Install iam system with all its components.
    swagger            Generate swagger document.
    tools              install dependent tools.

    # 帮助命令
    help               Show this help info.

  # 选项
  Options:
    DEBUG        Whether to generate debug symbols. Default is 0.
    BINS         The binaries to build. Default is all of cmd.
                 This option is available when using: make build/build.multiarch
                 Example: make build BINS="iam-apiserver iam-authz-server"
    ...
  ```

#### 设计合理的 Makefile 结构

- 推荐的 Makefile 结构
  - 采用分层的设计方法
    - 根目录下的 Makefile 聚合所有的 Makefile 命令
    - 具体实现则按功能分类，放在另外的 Makefile 中
  - Makefile 与 shell 脚本分离
    - 可以将复杂的 shell 命令封装在 shell 脚本中，供 Makefile 直接调用
    - 一些简单的命令则可以直接集成在 Makefile 中

  ```text

  ├── Makefile
  ├── scripts
  │   ├── gendoc.sh
  │   ├── make-rules
  │   │   ├── gen.mk
  │   │   ├── golang.mk
  │   │   ├── image.mk
  │   │   └── ...
      └── ...
  ```

- 目标命名技巧
  - 为了跟 Makefile 的层级相匹配，golang.mk 中的所有目标都按go.xxx这种方式命名。
  - 通过这种命名方式，我们可以很容易分辨出某个目标完成什么功能，放在什么文件里，这在复杂的 Makefile 中尤其有用。

#### 掌握 Makefile 编写技巧

##### 技巧1：善用通配符和自动变量

- Makefile 允许对目标进行类似正则运算的匹配，主要用到的通配符是%。

- 通过使用通配符，可以使不同的目标使用相同的规则，从而使 Makefile 扩展性更强，也更简洁。

- 举例

  ```make
  # iam/scripts/make-rules/tools.mk
  tools.verify.%:
    @if ! which $* &>/dev/null; then $(MAKE) tools.install.$*; fi
  ```

##### 技巧3：依赖需要用到的工具

- 在目标的依赖中包含工具
  - 如果 Makefile 某个目标的命令中用到了某个工具，可以将该工具放在目标的依赖中。
  - 这样，当执行该目标时，就可以指定检查系统是否安装该工具，如果没有安装则自动安装，从而实现更高程度的自动化。

- 举例

  ```make
  .PHONY: format
  format: tools.verify.golines tools.verify.goimports
    @echo "===========> Formating codes"
    @$(FIND) -type f -name '*.go' | $(XARGS) gofmt -s -w
    @$(FIND) -type f -name '*.go' | $(XARGS) goimports -w -local $(ROOT_PACKAGE)
    @$(FIND) -type f -name '*.go' | $(XARGS) golines -w --max-len=120 --reformat-tags --shorten-comments --ignore-generated .
  ```

##### 技巧5：编写可扩展的 Makefile

- 可扩展的 Makefile 的含义
  - 可以在不改变 Makefile 结构的情况下添加新功能。
  - 扩展项目时，新功能可以自动纳入到 Makefile 现有逻辑中。

- 如何编写可扩展的 Makefile
  - 通过设计合理的 Makefile 结构来实现。
  - 编写 Makefile 时采用一定的技巧，例如多用通配符、自动变量、函数等。

##### 技巧7：使用带层级的命令方式

- 使用带层级的命令方式的好处
  - 当 Makefile 有大量目标时，通过分组，我们可以更好地管理这些目标。
  - 其次，分组也能方便理解，可以通过组名一眼识别出该目标的功能类别。
  - 最后，这样做还可以大大减小目标重名的概率。

##### 技巧8：做好目标划分

- 目标划分的例子
  - 比如，我们可以将安装工具拆分成两个目标：验证工具是否已安装和安装工具。

- 目标划分的好处
  - 通过这种方式，可以给我们的 Makefile 带来更大的灵活性。
    例如：我们可以根据需要选择性地执行其中一个操作，也可以两个操作一起执行。

##### 技巧9：设置 OPTIONS

- 举例：通过选项 V 来控制是否需要在执行 Makefile 时打印详细的信息。

  ```make
  ifndef V
  MAKEFLAGS += --no-print-directory
  endif
  ```

##### 技巧10：定义环境变量

- 这些环境变量和编程中使用宏定义的作用是一样的：
  只要修改一处，就可以使很多地方同时生效，避免了重复的工作。

- 通常，我们可以将 GO、GO_BUILD_FLAGS、FIND 这类变量定义为环境变量。

##### 技巧11：自己调用自己

- 在编写 Makefile 的过程中，你可能会遇到这样一种情况：
  - A-Target 目标命令中，需要完成操作 B-Action
  - 操作 B-Action 我们已经通过伪目标 B-Target 实现过
  - 为了达到最大的代码复用度，这时候最好的方式是在 A-Target 的命令中执行 B-Target

  ```make
  tools.verify.%:
    @if ! which $* &>/dev/null; then $(MAKE) tools.install.$*; fi
  ```

#### 总结

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

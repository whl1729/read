# 《Go 语言项目开发实战》分析笔记

## 第15章 研发流程实战：IAM 项目是如何进行研发流程管理的？

### Q1：这一章的内容属于哪一类别？

计算机/软件工程。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- 开发阶段
  - 代码开发
  - 代码提交
- 测试阶段
- IAM 项目的 Makefile 项目管理技巧
  - help 自动解析
  - Options 中指定变量值
  - 自动生成 CHANGELOG
  - 自动生成版本号
  - 保持行为一致
- 总结

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 开发阶段

- 代码开发的具体步骤
  - 新建功能分支
  - 自动生成代码
  - 版权检查
  - 代码格式化
  - 静态代码检查
  - 单元测试
  - 构建

#### 测试阶段

- 删除 feature 分支
  - 我们的代码都合并入 master/develop 分支后，feature 开发者可以选择是否要保留 feature。
  - 如果没有特别的原因，我建议删掉，因为 feature 分支太多的话，不仅看起来很乱，还会影响性能。
  - 删除操作如下

  ```bash
  # delete local branch
  git branch -d feature/helloworld

  # delete remote branch
  git push -d origin feature/helloworld
  ```

#### IAM 项目的 Makefile 项目管理技巧

- help 自动解析
  - 自动解析 Makefile 中 `##` 开头的注释行，从而自动生成 make help 输出。

- Options 中指定变量值

- 自动生成 CHANGELOG
  - 借助工具：`git-chglog`

- 自动生成版本号
  - 借助工具：`gsemver`
  - 使用脚本自动打上版本号标签

  ```bash
  version=v`gsemver bump`
  if [ -z "`git tag -l $version`" ];then
    git tag -a -m "release version $version" $version
  fi
  ```

- 保持行为一致
  - 不管使用手动操作，还是通过 Makefile 操作，都要确保
    git commit message 规范检查结果、生成的 CHANGELOG、生成的版本号是一致的。
  - 这需要我们采用同一种操作方式。

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

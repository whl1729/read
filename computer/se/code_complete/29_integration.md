# 《Code Complete》分析笔记

## Chapter 29: Integration

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Importance of the Integration Approach
  - Affect the order in which classes are designed, coded, and tested
  - A well-thought-out integration order reduces testing effort and eases debugging.
- Integration Frequency: Phased or Incremental?
  - Unless the project is trivial, Incremental is better than phased.
- Incremental Integration Strategies
  - Top-Down Integration
  - Bottom-Up Integration
  - Sandwich Integration
  - Risk-Oriented Integration
  - Feature-Oriented Integration
  - T-Shaped Integration
- Daily Build and Smoke Test
  - Guidelines for Daily Build
  - What kinds of projects can use the daily build process
  - continous integration frequency: daily or more frequent?

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

#### 29.4 Daily Build and Smoke Test

- Guidelines for daily build
  - Build daily
  - Check for broken builds
  - Smoke test daily
  - Keep the smoke test current
  - Automate the daily build and smoke test
  - Establish a build group
  - Add revisions to the build only when it makes sense to do so...
  - ...but don't wait too long to add a set of revisions
  - Require developers to somke test their code before adding it to the system
  - Cretae a holding area for code that's to be added to the build
  - Create a penalty for breaking the build
  - Release builds in the morning
  - Build and smoke test even under pressure

- The larger the project, the more important incremental integration becomes.

- For most projects, I think literal continuous integration is too much of a good thing.
  (Literal continuous integration: integrate each change with the latest build every couple of hours.)

#### 29.5 Checklist: Integration

- Integration Strategy
  - [ ] Does the strategy identify the optimal order in which subsystems, classes, and routines should be integrated?
  - [ ] Is the integration order coordinated with the construction order so that classes will be ready for integration at the right time?
  - [ ] Does the strategy lead to easy diagnosis of defects?
  - [ ] Does the strategy keep scaffolding to a minimum?
  - [ ] Is the strategy better than other approaches?
  - [ ] Have the interfaces between components been specified well?
        (Specifying interfaces isn’t an integration task, but verifying that they have been specified well is.)

- Daily Build and Smoke Test
  - [ ] Is the project building frequently—ideally, daily—to support incremental integration?
  - [ ] Is a smoke test run with each build so that you know whether the build works?
  - [ ] Have you automated the build and the smoke test?
  - [ ] Do developers check in their code frequently—going no more than a day or two between check-ins?
  - [ ] Is the smoke test kept up to date with the code, expanding as the code expands?
  - [ ] Is a broken build a rare occurrence?
  - [ ] Do you build and smoke test the software even when you’re under pressure?

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

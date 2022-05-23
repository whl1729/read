# 《Code Complete》分析笔记

## Chapter 28: Managing Constrution

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Encouragaing good coding
  - Assign two people to every part of the project
  - Review every line of code
  - Require code sign-offs
  - Route good code examples for review
  - Emphasize that code listings are public assets
  - Reward good code
  - One easy standard
- Configuration management
  - What is Configuration Management
  - Requirements and design changes
  - Software code changes
  - Tool versions
  - Machine configurations
  - **Backup plan**
- Estimating a construction schedule
  - Estimation approaches
  - Estimating the amount of construction
  - Influences on schedule
  - Estimation vs control
  - What to do if you're behind
- Measurement
- Treating programmers as people
  - How do programmers spend their time?
  - Variation in performance and quality
  - Individual variation
  - Team variation
  - Religious issues
  - Physical environment
- Managing your manager

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

- configuration management
  - The practice of identifying project artifacts and handling changes systematically
    so that a system can maintain its integrity over time.
  - Another name for it is "change control."
    It includes techniques for evaluating proposed changes, tracking changes,
    and keeping copies of the system as it existed at various points in time.

### Q5：这一章的关键句是什么？

#### 28.2 Checklist for Configuration Management

- General
  - [ ] Is your software configuration management plan designed to help programmers and minimize overhead?
  - [ ] Does your SCM approach avoid overcontrolling the project?
  - [ ] Do you group change requests, either through informal means (such as a list of pending changes)
        or through a more systematic approach (such as a change-control board)?
  - [ ] Do you systematically estimate the cost, schedule, and quality impact of each proposed change?
  - [ ] Do you view major changes as a warning that requirements development isn’t yet complete?

- Tools
  - [ ] Do you use version-control software to facilitate configuration management?
  - [ ] Do you use version-control software to reduce coordination problems of working in teams?

- Backup
  - [ ] Do you back up all project materials periodically?
  - [ ] Are project backups transferred to off-site storage periodically?
  - [ ] Are all materials backed up, including source code, documents, graphics, and important notes?
  - [ ] Have you tested the backup-recovery procedure?

#### 28.3 Estimating a construction schedule

- Estimation Approaches
  - Use estimating software.
  - Use an algorithmic approach, such as Cocomo II, Barry Boehm’s estimation model (Boehm et al. 2000).
  - Have outside estimation experts estimate the project.
  - Have a walk-through meeting for estimates.
  - Estimate pieces of the project, and then add the pieces together.
  - Have people estimate their own tasks, and then add the task estimates together.
  - Refer to experience on previous projects.
  - Keep previous estimates and see how accurate they were. Use them to adjust new estimates.

- Steps to estimating a project
  - Establish objectives
  - Allow time for the estimate, and plan it
  - Spell out software requirements
  - Estimate at a low level of detail
  - Use several different estimation techniques, and compare the results
  - Reestimate periodically

#### 28.6 Managing your manager

- Approaches to dealing with your manager
  - Plant ideas for what you want to do, and then wait for your manager
    to have a brainstorm (your idea) about doing what you want to do.
  - Educate your manager about the right way to do things.
    This is an ongoing job because managers are often promoted, transferred, or fired.
  - Focus on your manager’s interests, doing what he or she really wants you to do,
    and don’t distract your manager with unnecessary implementation details.
    (Think of it as “encapsulation” of your job.)
  - Refuse to do what your manager tells you, and insist on doing your job the right way.
  - Find another job.

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？

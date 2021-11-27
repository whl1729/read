# 《Code Complete》分析笔记

## Chapter 27: How Program Size Affects Construction

### Q1：这一章的内容是什么？

### Q2：这一章的大纲是什么？

- Communication and size
  - Communication paths
  - Documents
- Range of project sizes
  - The size of a project team
- Effect of project size on errors
  - The density of defects increases
- Effect of project size on productivity
- Effect of project size on Development activities
  - Activity proportions and size
  - Programs, products, systems, and system products
  - Methodology and size
    - Formal documentation
    - Right-weight methodology

### Q3：作者想要解决什么问题？

### Q4：这一章的关键词是什么？

### Q5：这一章的关键句是什么？

#### 27.1 Communication and size

- The more communication paths you have,
  the more time you spend communicating and 
  the more opportunities are created for communication mistakes.

- The typical approach taken to streamlining communication is
  to formalize it in documents.

#### 27.3 Effect of project size on errors

- The number of errors increases dramatically as project size increases,
  with very large projects having up to four times as many errors per thousand lines of code as small projects.

#### 27.4 Effect of project size on productivity

- As project size increases,
  team size and organization become greater influences on productivity.

- All other things being equal,
  productivity will be lower on a large project than on a small one

#### 27.5 Effect of project size on Development activities

- As project size increases,
  construction becomes a smaller part of the total effort.

- A list of activities that grow at a more-than-linear rate as project size increases:
  - Communication
  - Planning
  - Management
  - Requirements development
  - System functional design
  - Interface design and specification
  - Architecture
  - Integration
  - Defect removal
  - System testing
  - Document production

- Different kinds of software
  - Program
    - Used by itself by the person who developed it or, informally, by a few others.
  - Software product
    - Used by people other than the original developer.
    - Used in environments that differ from the environment in which the product was created. 
  - Software system
    - A group of programs that work together.
  - System product
    - Polish of a product and the multiple parts of a system.

- A common cause of estimation errors
  - A failure to appreciate the differences in polish and complexity among programs, products, systems, and system products 

- Another cause of estimation errors
  - As you scale up, construction becomes a smaller part of the total effort in a project.
  - If you base your estimates solely on construction experience, the estimation error increases.

- Methodology
  - The more formal the project, the more paper you have to generate to make sure you’ve done your homework.
  - Consider your project’s specific size and type and then find the methodology that's "right-weight."

### Q6：作者是怎么论述的？

### Q7：作者解决了什么问题？

### Q8：我有哪些疑问？

### Q9：这一章说得有道理吗？为什么？

### Q10：如何拓展这一章？

#### Q10.1：为什么是这样的？为什么发展成这样？为什么需要它？

#### Q10.2：有哪些相似的知识点？它们之间的联系是什么？

#### Q10.3：其他领域/学科有没有相关的知识点？日常生活中有没有类似的现象？

### Q11：这一章和我有什么关系？


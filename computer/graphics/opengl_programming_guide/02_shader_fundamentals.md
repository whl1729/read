# 《OpenGL Programming Guide》分析笔记

## Chapter 2: Shader Fundamentals

### Q1：这一章的内容属于哪一类别？

计算机图形学/OpenGL。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### An Overview of the OpenGL Shading Language

- Storage Oualifiers
  - `in` Specifies that the variable is an input to the shader stage.
  - `out` Specifies that the variable is an output from a shader stage.
  - `uniform` Specifies that the value is passed to the shader from the application and 
    is constant across a given primitive.
  - `buffer` Specifies read-write memory shared with the application.

- Create an executable shader program
  - For each shader object
    - `glCreateShader`: Create a shader object
    - Compile your shader source into the object
      - `glShaderSource`: Associate the source code of the shader with the created object.
      - `glCompileShader`: Compiles the source code for shader.
    - Verify that your shader compiled successfully.
  - Then, to link multiple shader objects into a shader program, you'll
    - Create a shader program.
    - `glAttachShader` Attach the appropriate shader objects to the shader program.
    - `glLinkProgram` Link the shader program.
    - Verify that the shader link phase completed successfully.
    - `glUseProgram` Use the shader for vertex or fragment processing.

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


# 《WebGL Programming Guide》分析笔记

## Chapter 03: Drawing Multiple Points

### Q1：这一章的内容属于哪一类别

计算机图形学

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- Drawing Multiple Points
- Hello Triangle
- Moving, Rotating, and Scaling

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

- buffer object
  - A memory area that can store multiple vertices in the WebGL system.
  - It is used both as a staging area for the vertex data and
    a way to simultaneously pass the vertices to a vertex shader.

### Q6：这一章的关键句是什么

- By creating a buffer object and then writing the vertices to the object,
  you can pass multiple vertices to a vertex shader through one of its attribute variables.

- 5 steps to pass multiple data values to a vertex shader through a buffer object.
  - Create a buffer object (`gl.createBuffer()`).
  - Bind the buffer object to a target (`gl.bindBuffer()`).
  - Write data into the buffer object (`gl.bufferData()`).
  - Assign the buffer object to an attribute variable (`gl.vertexAttribPointer()`).
  - Enable assignment (`gl.enableVertexAttribArray()`).

- `Float32Array` vs `Array`
  - The standard array in JavaScript is a general-purpose data structure able to hold both numeric data and strings
    but isn’t optimized for large quantities of data of the same type, such as vertices.
  - To address this issue, the typed array such as Float32Array, has been introduced.

- `Window.requestAnimationFrame(callback)`
  - Tells the browser that you wish to perform an animation and
    requests that the browser calls a specified function to update an animation before the next repaint.
  - The method takes a callback as an argument to be invoked before the repaint.
  - requestAnimationFrame() is 1 shot.
    Your callback routine must itself call requestAnimationFrame() again if you want to animate another frame at the next repaint.

- Pass information to the vertex shader
  - By creating a buffer object for each type of data in this way and then allocating it to the attribute variables,
    you can pass several pieces of information about each vertex to the vertex shader.
  - Other types of information that can be passed include color, texture coordinates, and normals, as well as point size.

### Q7：作者是怎么论述的

### Q8：作者解决了什么问题

### Q9：我有哪些疑问

### Q10：这一章说得有道理吗？为什么

### Q11: 这一章讨论的知识的本质是什么

### Q12: 这一章讨论的知识的第一原则是什么

### Q13：这一章讨论的知识的结构是怎样的

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

### Q15：有哪些相似的知识？它们之间的联系是什么

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

### Q17: 这一章对我有哪些用处/帮助/启示

### Q18: 我如何应用这一章的知识去解决问题

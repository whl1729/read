# 《WebGL Programming Guide》分析笔记

## Chapter 02: Your First Step with WebGL

### Q1：这一章的内容属于哪一类别

计算机图形学

### Q2：这一章的内容是什么

### Q3：这一章的大纲是什么

- What is a canvas?
- The world's shortest WebGL program: Clear Drawing Area
- Draw a point (version 1)
- Draw a point (version 2)
- Draw a point with a mouse click
- Change the point color

### Q4：作者想要解决什么问题

### Q5：这一章的关键词是什么

- canvas
  - A HTML tag that offers a convenient way to draw computer graphics dynamically using JavaScript.

### Q6：这一章的关键句是什么

#### What is a canvas

- Using the `<canvas>` tag
  - id
  - width
  - height
  - display error message if the browser doesn't support `<canvas>`

- The coordinate system of the `<canvas>` element
  - The horizontal direction as the x-axis (right-direction is positive)
  - The vertical direction as the y-axis (down-direction is positive)
  - The origin is located at the upper-left corner

#### Draw a Point (Version 1)

- Two types of shaders
  - Vertex shader
    - Vertex shaders are programs that describe the traits (position, colors, and so on) of a vertex.
    - The vertex is a point in 2D/3D space, such as the corner or intersection of a 2D/3D shape.
  - Fragment shader
    - A program that deals with per-fragment processing such as lighting.
    - The fragment is a WebGL term that you can consider as a kind of pixel (picture element).

- The WebGL Coordinate System
  - Right-handed coordinate system: (right, top, front)
  - WebGL maps the coordinate system to the area as follows:
    - The center position of a `<canvas>`: (0.0, 0.0, 0.0)
    - The two edges of the x-axis of the `<canvas>`: (-1.0, 0.0, 0.0) and (1.0, 0.0, 0.0)
    - The two edges of the y-axis of the `<canvas>`: (0.0, -1.0, 0.0) and (0.0, 1.0, 0.0)

#### Draw a Point (Version 2)

- Two ways to pass data to a vertex shader
  - attribute variable: passes data that differs for each vertex
  - uniform variable: passes data that is the same (or uniform) in each vertex.

#### canvas 2D api

- `canvas.getContext(contextType)` Possible values for `contextType`:
  - "2d"
  - "webgl"
  - "webgl2"
  - "bitmaprenderer"

- `ctx.fillStyle = color;`
  - A DOMString parsed as CSS `<color>` value
  - Example 1: `ctx.fillStyle = 'rgba(0, 0, 255, 1.0)'`

- `ctx.fillRect(x, y, width, height)`

- `ctx.fillText(text, x, y, [, maxWidth])`

### Q7：作者是怎么论述的

### Q8：作者解决了什么问题

### Q9：我有哪些疑问

#### Q9.1: 如何调用`gl.drawArrays(mode, first, count)`画直线或三角形

### Q10：这一章说得有道理吗？为什么

### Q11: 这一章讨论的知识的本质是什么

### Q12: 这一章讨论的知识的第一原则是什么

### Q13：这一章讨论的知识的结构是怎样的

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它

### Q15：有哪些相似的知识？它们之间的联系是什么

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象

### Q17: 这一章对我有哪些用处/帮助/启示

### Q18: 我如何应用这一章的知识去解决问题

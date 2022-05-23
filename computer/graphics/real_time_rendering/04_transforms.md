# 《Real-Time Rendering》分析笔记

## Chapter 4 Transforms

### Q1：这一章的内容属于哪一类别？

计算机图形学

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- Basic Transforms
- Special Matrix Transforms and Operations
- Quaternions
- Vertex Blending
- Morphing
- Geometry Cache Playback
- Projections

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

- Linear transform
  - One that preserves vector addition and scalar multiplication. Specifically,

  ```js
  f(x) + f(y) = f(x + y)
  kf(x) = f(kx)
  ```

- Affine transform
  - One that performs a linear transform and then a translation.
  - All translation, rotation, scaling, reflection, and shearing matrices are affine.
  - The main characteristic of an affine matrix is that it preserves the parallelism of lines, but not necessarily lengths and angles.

- Orthographic Projection
  - Parallel lines remain parallel after the projection.
  - Objects maintain the same size regardless of distance to the camera.

- Perspective Projection (透视投影、中心投影)
  - Parallel lines are generally not parallel after projection; rather, they may converge to a single point at their extreme.
  - Perspective more closely matches how we perceive the world, i.e., objects farther away are smaller.

- axis-aligned bounding box (AABB)

- canonical view volume
  - In OpenGL the axis-aligned cube has a minimum corner of (−1, −1, −1) and a maximum corner of (1, 1, 1).
  - In DirectX the bounds are (−1, −1, 0) to (1, 1, 1).
  - This cube is called the canonical view volume.

- normalized device coordinates
  - The coordinates in canonical view volume are called normalized device coordinates.

### Q6：这一章的关键句是什么？

#### 4.1 Basic Transforms

- A direction vector is represented as `v = (vx vy vz 0)T` and a point as `v = (vx vy vz 1)T`.

#### 4.7 Projections

- The reason for transforming into the canonical view volume
  - Clipping is more efficiently performed there.

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

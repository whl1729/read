# 《Real-Time Rendering》分析笔记

## Chapter 2 The Graphics Rendering Pipeline

### Q1：这一章的内容属于哪一类别？

计算机图形学

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- Architecture
- The Application Stage
- Geometry Processing
- Rasterization
- Pixel Processing
- Through the Pipeline

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

- space or coordinate systems
  - model space
    - Originally, a model resides in its own model space, which simply means that it has not been transformed at all.
  - world space
  - view space / camera space / eye space

- coordinates
  - model coordinates
  - world coordinates
  - eye coordinates
  - clip coordinates
    - After orthographic or perspective transform, the models are said to be in clip coordinates.
    - These are in fact homogeneous coordinates.
  - screen coordinates
  - window coordinates

- transform
  - model transform
    - Each model can be associated with a model transform so that it can be positioned and oriented.
    - It is the vertices and the normals of the model that are transformed by the model transform.
  - view transform
    - To facilitate projection and clipping, the camera and all the models are transformed with the view transform.
    - The purpose of the view transform is to place the camera at the origin and aim it,
      to make it look in the direction of the negative z-axis, with the y-axis pointing upward and the x-axis pointing to the right.

> 伍注：变换包括位置和方向两方面。方向可以用法向量来表示。

- shading
  - This operation of determining the effect of a light on a material is known as shading.
  - It involves computing a shading equation at various points on the object.
  - Typically, some of these computations are performed during geometry processing on a model’s vertices,
    and others may be performed during per-pixel processing.

- view volume
- canonical view volume

- tessellation
  - With tessellation, a curved surface can be generated with an appropriate number of triangles.

### Q6：这一章的关键句是什么？

#### 2.0 Preface

- The main function of the rendering pipeline
  - to generate, or render, a two-dimensional image, given a virtual camera, three-dimensional objects, light sources, and more.

> 伍注：渲染过程涉及三大部件：物体、照相机、光源。

- The locations and shapes of the objects in the image are determined by
  - their geometry, the characteristics of the environment, and the placement of the camera in that environment.

> 伍注：物体的位置和形状由物体的几何形状、环境特性和照相机的放置（包括位置和角度）确定。
> Question: 这里如何理解环境特性对物体的位置和形状的影响？

- The appearance of the objects is affected by
  - material properties, light sources, textures (images applied to surfaces), and shading equations.

#### 2.1 Architecture

- 4 main stages of the real-time rendering pipeline:
  - Application
  - Geometry processing
  - Rasterization
  - Pixel processing

- Application stage
  - Driven by the application and is therefore typically implemented in software running on general-purpose CPUs.
  - Examples: collision detection, global acceleration algorithms, animation, physics simulation, and many others.

- Geometry processing stage
  - Computes what is to be drawn, how it should be drawn, and where it should be drawn.
  - Deals with transforms, projections, and all other types of geometry handling.

- Rasterization
  - Takes as input three vertices,
    forming a triangle,
    and finds all pixels that are considered inside that triangle,
    then forwards these to the next stage.

- Pixel Processing
  - Executes a program per pixel to determine its color and may perform depth testing to see whether it is visible or not.
  - It may also perform per-pixel operations such as blending the newly computed color with a previous color.

#### 2.2 The Application Stage

- Changes in the application stage can also affect the performance of subsequent stages.
  - For example, an application stage algorithm or setting could decrease the number of triangles to be rendered.

- Compute shader
  - Some application work can be performed by the GPU, using a separate mode called a compute shader.
  - This mode treats the GPU as a highly parallel general processor, ignoring its special functionality meant specifically for rendering graphics.

- At the end of the application stage,
  - the geometry to be rendered is fed to the geometry processing stage.
  - These are the rendering primitives, i.e., points, lines, and triangles, that might eventually end up on the screen.

#### 2.3 Geometry Processing

- This geometry processing stage is further divided into a pipeline of functional stages:
  - vertex shading -> projection -> clipping -> screen mapping

##### 2.3.1 Vertex Shading

- Two main tasks of vertex shading
  - to compute the position for a vertex
  - to evaluate whatever the programmer may like to have as vertex output data, such as a normal and texture coordinates.

- Why it's called "Vertex Shading" (History)
  - Traditionally much of the shade of an object was computed by applying lights to each vertex's location and normal
    and storing only the resulting color at the vertex.
  - These colors were then interpolated across the triangle.
  - For this reason, this programmable vertex processing unit was named the vertex shader.
  - With the advent of the modern GPU, along with some or all of the shading taking place per pixel,
    this vertex shading stage is **more general** and may not evaluate any shading equations at all, depending on the programmer’s intent.
  - The vertex shader is now a more general unit dedicated to setting up the data associated with each vertex.

> 伍注：以前 Vertex shading 阶段主要是对顶点进行着色，现在变得更通用了——创建顶点相关数据，而不一定是着色。

- Vertex data: A variety of material data can be stored at each vertex, such as
  - the point’s location, a normal, a color, or any other numerical information that is needed to evaluate the shading equation.

- Vertex shading results
  - which can be colors, vectors, texture coordinates, along with any other kind of shading data
  - are then sent to the rasterization and pixel processing stages to be interpolated and used to compute the shading of the surface.

- As part of vertex shading, rendering systems perform projection and then clipping,
  - which transforms the view volume into a unit cube with its extreme points at (−1, −1, −1) and (1, 1, 1).
  - The unit cube is called the canonical view volume.

- Orthographic Projection
  - The view volume of orthographic viewing is normally a rectangular box,
  - The view volume is transformed into the unit cube.
  - This transformation is a combination of a translation and a scaling.

- Perspective Projection
  - The view volume, called a frustum, is a truncated pyramid with rectangular base.
  - The frustum is also transformed into the unit cube.

##### 2.3.2 Optional Vertex Processing

- Tessellation
  - The tessellation stage consists of a series of stages itself—
    hull shader, tessellator, and domain shader—
    that converts these sets of patch vertices into (normally) larger sets of vertices that are then used to make new sets of triangles.
  - The camera for the scene can be used to determine how many triangles are generated: many when the patch is close, few when it is far away.

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

#### Q9.1: 如何理解环境特性对物体被渲染后的位置和形状的影响？

#### Q9.2: 为什么 view space 的坐标系方向会让修剪（clipping）和投影（projection）更简单？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

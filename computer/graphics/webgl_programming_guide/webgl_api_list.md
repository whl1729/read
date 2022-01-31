# WebGL API List

- `void gl.clearColor(red, green, blue, alpha)`
  - Specifies the color values used when clearing color buffers.
  - Once you specify the clear color,
    the color is retained in the WebGL system and not changed until another color is specified by a call to gl.clearColor().
    This means you don’t need to specify the clear color again if at some point in the future you want to clear the area again using the same color.

- `void gl.clear(mask)` Possible values for `mask`:
  - gl.COLOR_BUFFER_BIT
  - gl.DEPTH_BUFFER_BIT
  - gl.STENCIL_BUFFER_BIT

- `void gl.drawArrays(mode, first, count)` Possible values for `mode`:
  - gl.POINTS: Daws a single dot.
  - gl.LINE_STRIP: Draws a straight line to the next vertex.
  - gl.LINE_LOOP: Draws a straight line to the next vertex, and connects the last vertex back to the first.
  - gl.LINES: Draws a line between a pair of vertices.
  - gl.TRIANGLE_STRIP
  - gl.TRIANGLE_FAN
  - gl.TRIANGLES: Draws a triangle for a group of three vertices.

- `GLINT gl.getAttribLocation(program, name)`
  - Returns the location of an attribute variable in a given WebGLProgram.

- `gl.vertexAttrib[1234]f(index, v0, v1, v2, v3)` or `gl.vertexAttrib[1234]f[v](index, value)`
  - Specify constant values for generic vertex attributes

> 伍注：以下关于缓冲区的接口的解释，可以查阅 webglpg 第3章。

- `gl.createBuffer()`
  - Creates and initializes a WebGLBuffer storing data such as vertices or colors.

> 伍注：创建一个缓冲区。

- `gl.bindBuffer(target, buffer)`
  - Binds a given WebGLBuffer to a target.
  - `target`: A GLenum specifying the binding point (target). Possible values:
    - `gl.ARRAY_BUFFER`
    - `gl.ELEMENT_ARRAY_BUFFER`
  - `buffer`: A WebGLBuffer to bind.

> 伍注：将缓冲区地址赋值给全局指针变量。

- `gl.bufferData(target, size, usage)` or `gl.bufferData(target, srcData, usage)`
  - Initializes and creates the buffer object's data store.
  - `usage`: A GLenum specifying the intended usage pattern of the data store for optimization purposes.
    - `gl.STATIC_DRAW`
    - `gl.DYNAMIC_DRAW`
    - `gl.STREAM_DRAW`

> 伍注：为缓冲区分配内存，并将源数据拷贝到缓冲区。

- `gl.vertexAttribPointer(index, size, type, normalized, stride, offset)`
  - `index`: A GLuint specifying the index of the vertex attribute that is to be modified.
  - `size`: A GLint specifying the number of components per vertex attribute. Must be 1, 2, 3, or 4.
  - `type`: A GLenum specifying the data type of each component in the array.
    - `gl.BYTE`
    - `gl.SHORT`
    - `gl.UNSIGNED_BYTE`
    - `gl.UNSIGNED_SHORT`
    - `gl.FLOAT`
  - `normalized`: A GLboolean specifying whether integer data values should be normalized into a certain range when being cast to a float.
  - `stride`: A GLsizei specifying the offset in bytes between the beginning of consecutive vertex attributes.
  - `offset`: A GLintptr specifying an offset in bytes of the first component in the vertex attribute array.

> 伍注：将缓冲区指针赋值给属性变量，
> 并指定怎样从缓冲区取数据：每次取几个数据、每个数据有多大。

- `gl.enableVertexAttribArray(index)`
  - Turns on the generic vertex attribute array at the specified index into the list of attribute arrays.
  - `index`: A GLuint specifying the index number that uniquely identifies the vertex attribute to enable.

> 伍注：使能从缓冲区取数据赋值给属性变量。

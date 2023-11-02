# mesh shader

## 定义
The mesh shader stage produces triangles for the rasterizer, but uses a cooperative thread model internally instead of using a single-thread program model, similar to compute shaders.

task shader -> mesh shader

task shader uses a cooperative thread model. the input and output of task shader is user defined.
which is different.

## Mesh Shading Pipeline
A new, two-stage pipeline alternative supplements the classic attribute fetch, vertex, tessellation, geometry shader pipeline. This new pipeline consists of a task shader and mesh shader:

Task shader : a programmable unit that operates in workgroups and allows each to emit (or not) mesh shader workgroups

Mesh shader : a programmable unit that operates in workgroups and allows each to generate primitives

The optional expansion via task shaders allows early culling of a group of primitives or making LOD decisions upfront.


## meshlet buffer structure

meshlet vertices: start length 每一个meshlet 中的index value都是独一无二的

meshlet primitives : local index buffer 可以服用顶点对应meshlet vertices中的local index

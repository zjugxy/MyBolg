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



## mesh shader glsl

layout(local_size_x = 32) in; //the number of threads per workgroup

layout(triangles) out;//points lines triangles

layout(max_vertices=64,max_primitives=126) out;

//可以使用NV_fragment_shader_barycentric手动重心坐标插值，从而更好地pack坐标值啥的--important


# drawmeshtaskNV(uint first, uint count)

    The x component of gl_WorkGroupID of the first active stage  will be within
    the range of [<first> , <first + count - 1>]. The y and z component of
    gl_WorkGroupID within all stages will be set to zero.



# mesh shader glsl输入
可以简单的认为mesh shader的输入只有两个

第一个 ***gl_WorkGroupID.x*** 由 **gl_DrawMeshTaskNV(first,cnt)**决定范围为first --> first+cnt -1

第二个参数是 ***gl_LocalInvocationID.x*** ,由 **layout(local_size_x=thread_num)in;** 决定


# shader 



# 参考文献
https://registry.khronos.org/OpenGL/extensions/NV/NV_mesh_shader.txt

https://github.com/KhronosGroup/GLSL/blob/master/extensions/nv/GLSL_NV_mesh_shader.txt


# Geometry encode

## pre wire local coordinate frame

1. all the meshlet are constructed with planarity in mind. the average orthogonal distance to the fitted plane is very small.

x-axis is the normal of plane, and is x-axis of local coordianate frame.

//note: 这里的意思是将顶点从x轴投影。选取多个y,z坐标轴，选取sum最小的，从而使得编码范围尽可能小。
sample multiple rotations of the coordinate system around x-axis.
choose the sum which is minimized. in this way, we determine the final x,y,z axis.

//transformation

1. determinethe origin, and scale the point  into a unit local coordinates.




## mesh shader precedure

1. 每一个mesh shader对应一个meshlet，对于每一个meshlet。mesh shader都会launch32个线程来处理

step1: dequantize the local coordinate into global coordinate.

step2: triangel indices generate. 读取left right ringtable --> i,i+1 mode mring ,L[i] or R[i]

step3: vertex decode. calculate offset --> transform into global coordinate --> view_projection tranform  --> write to output





## 实现的想法

首先导入openmesh当中。

随后划分meshlet，使用face prop in openmesh，确定每一个face对应的meshlet id,并将每个meshlet对应的face单独存储起来

对于边界wire处理，查看左右两侧的faceprop是不是相等，不相等则是边界边，使用left right???组合判断是不是同一对meshlet的情况。

//对边界边进行render,对meshlet进行render



随后就是要处理
//使用gpu并行压缩。

//关键的point这个end to end方法似乎只是用于渲染的？？

思考
//无论如何你在render的时候都是要解压缩格式的mesh
//唯一有可能的就是几何和连接关系数据分开，然后连接关系是一个random access的或者是可以在gpu中并行快速解压缩的
//使用这个文章中提到的对geometry data encode的方法我个人认为是十分耗时的
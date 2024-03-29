# window surface

窗口系统是基于操作系统的，而vulkan是跨平台的API，因而需要window　surface

我们需要使用 window system integration to establish the connection between vulkan and window system

## swap chain 

**The swap chain is essentially a queue of images** that are waiting to be presented to the screen. Our application will acquire such an image to draw to it, and then return it to the queue. How exactly the queue works and the conditions for presenting an image from the queue depend on how the swap chain is set up, but the general purpose of the swap chain is to synchronize the presentation of images with the refresh rate of the screen.

The input variable does not necessarily have to use the same name, they will be linked together using the indexes specified by the location directives

## shader module

a thin wrapper on the shader BYTECODE   也就是说shadre module是一个对shader 二进制code的包装,实际work的方法要在pipeline中才有

pipecreation完成之后就可以删除该shader module

## 创建流程

shader module --> shader stage creation


## viewport and scissor

viewport define the transformation from the image ato the framebuffer 

scsssor define which fragment should be stored in resitalization


## renderpass

We need to specify how many color and depth buffers there will be, how many samples to use for each of them and how their contents should be handled throughout the rendering operations. All of this information is wrapped in a render pass object
指定color depth buffer，samplers,contents

## command buffer

可以记录一系列的command到单个buffer中间,用于绘制framebuffer,并且command buffer可以复用于多个frames

    start render pass
        bind pipeline1 
        bind texture 4
        draw 100 vertices
    end render pass


## pipeline layout 

Pipeline Layout主要包含以下内容：

描述符集合（Descriptor Set）布局：
描述符集合是一组描述符的集合，描述了着色器程序中使用的资源。Pipeline Layout中定义了每个描述符集合的布局，包括描述符类型、绑定点、数组大小等信息。

着色器程序接口（Shader Interface）：
管线布局还包含了着色器程序的接口信息，包括着色器阶段（如顶点着色器、片段着色器等）中使用的输入、输出变量、uniform变量等的定义。

## queue family

图形渲染队列族：与图形渲染管线相关的硬件单元有关。这包括顶点处理单元、几何着色器、光栅化单元、片段着色器和输出合成等。

计算队列族：与通用计算任务相关的硬件单元有关。这包括计算单元、着色器核心和存储器等。

传输队列族：与数据传输和内存操作相关的硬件单元有关。这包括内存控制器、缓存和数据传输引擎等。

请注意，具体显卡的硬件架构和实现可能会有所不同，不同厂商的显卡可能会有不同类型和数量的队列族。因此，队列族与实际硬件部分的对应关系可能会有所变化。

使用多个队列族的目的是为了充分利用显卡的并行计算能力，使不同类型的任务可以在不同的硬件单元上并行执行，从而提高整体的性能和效率。这种并行执行的设计可以使显卡在处理多个任务时更加高效，并且允许应用程序在不同类型的任务之间进行任务调度和优化。


## swap chain创建逻辑

swap chain用于应用程序与窗口系统交互 swap chain将图片提交给surface（窗口系统）窗口系统是对显示器的封装

1. physical device 查询是否支持swap chain support
2. 在logical device 中enable对swap chain的support
3. 要查询我的swap chain support是否与surface compatible 先查询在（评分）最后设置

    1. Basic surface capabilities (min/max number of images in swap chain, min/max width and height of images)

    2. Surface formats (pixel format, color space)

    3. Available presentation modes

4. 为swap chain选择合适的设置
    1. format and color space:
    2. presentmode  mailbox替补掉未显示的image因而最多chain中间有两个image fifo阻塞（queue满了，application就需要等待）
    3. 确定swap chain的image extent

5. 选好这三个设置之后就可以填充swap chain create info  --> 同时在里面也要设置swap chain image的create info 并获取swapchainimage的handle

## image View 创建逻辑

An image view is quite literally a view into an image. It describes how to access the image and which part of the image to access, for example if it should be treated as a 2D texture depth texture without any mipmapping levels.




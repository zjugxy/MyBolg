# vulkan开发环境配置

## vulkan SDK

include headers,standard validation layers, debugging tools and loader for vulkan

## glfwpollevents

在一个典型的基于 GLFW 的应用程序中，通常会使用一个事件循环来不断调用 glfwPollEvents() 函数来处理 ***窗口事件*** 。这些事件可能包括键盘输入、鼠标移动、窗口大小改变等等。通过调用 glfwPollEvents()，应用程序能够及时响应用户输入并更新窗口的状态。

    // 主循环
    while (!glfwWindowShouldClose(window1) && !glfwWindowShouldClose(window2)) {
        // 处理窗口1的事件
        glfwMakeContextCurrent(window1);
        glfwPollEvents();

        // 处理窗口2的事件
        glfwMakeContextCurrent(window2);
        glfwPollEvents();

        // 渲染和更新逻辑
        // ...
    }


## glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API)

glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API)，我们告诉 GLFW 不要为窗口创建任何图形 API 相关的上下文

在使用glfwcreatewindow之前调用，防止生成opengl上下文
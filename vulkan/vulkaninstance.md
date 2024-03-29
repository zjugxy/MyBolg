# vulkan Instance

在Vulkan中，VkInstance是一个顶层对象，代表了Vulkan实例，它是使用Vulkan API进行图形渲染和计算的起始点。

VkInstance用于创建、配置和管理整个Vulkan实例的状态。它是使用Vulkan API的第一个步骤，通常是在应用程序启动时创建的。VkInstance包含了与Vulkan实例相关的信息和配置，例如应用程序的名称、版本号、所需的扩展和验证层等。

主要用途：

系统和硬件的初始化：创建VkInstance时，Vulkan会检查系统中可用的物理设备（如显卡），并进行初始化。这包括加载并验证驱动程序，检查硬件功能和性能等。

扩展和验证层的管理：VkInstance可以指定应用程序所需的Vulkan扩展和验证层。扩展提供了额外的功能和特性，而验证层用于调试和验证Vulkan操作的正确性。通过VkInstance，可以列出可用的扩展和验证层，并在创建设备时指定所需的扩展和验证层。

逻辑设备的创建：在创建VkInstance后，可以使用它来创建逻辑设备（VkDevice）。逻辑设备是与物理设备交互的接口，它可以用于创建和管理Vulkan资源，如缓冲区、纹理、渲染管线等。

全局状态的管理：VkInstance还包含全局状态，如全局内存分配器、全局回调函数等。这些全局状态在整个Vulkan应用程序中可见，可以用于自定义内存分配、错误处理和调试信息输出等。

总而言之，VkInstance是Vulkan应用程序的起始点，用于创建、配置和管理Vulkan实例的状态。它是与系统和硬件进行交互的接口，可以指定所需的扩展和验证层，并用于创建逻辑设备和管理全局状态。

vulkan instance相当于vulkan库对象，很顶层很抽象的一个东西用于管理整个vulkan的所有东西。

## validation layers

用于wrap没有check的函数，适用于debug模型

## logical device

After selecting a physical device to use we need to set up a logical device to interface with it. The logical device creation process is similar to the instance creation process and describes the features we want to use. We also need to specify which queues to create now that we've queried which queue families are available. You can even create multiple logical devices from the same physical device if you have varying requirements.

用于描述所需要的device的性质。

## queue and queue family需要重新仔细的理解


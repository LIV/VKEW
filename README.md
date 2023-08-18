# VKEW

Vulkan Extension Wrangler

VKEW is a single-header Vulkan Extension Wrangler, generated from the [Vulkan registry](https://raw.githubusercontent.com/KhronosGroup/Vulkan-Headers/main/registry/vk.xml)

This automates the task of calling `vkGetInstanceProcAddr()` and `vkGetDeviceProcAddr()` for every non-core function you may need, this does not replace, but instead complement, the usual way you access Vulkan on your platform.

Naming and general "way of working" is inspired by [GLEW](https://glew.sourceforge.net/). However, VKEW is a really small header-only library and do not interfere with the linking process

## How to use VKEW

```cpp

//Include Vulkan your usual way. Assuming from now all the necessary VULKAN_USE_PLATFORM macros are also defined
#include "vkew.h"


//Init VKEW for the current vulkan instance
vkewInitInstance(instance);

//Init VKEW for the current device
vkewInitDevice(device);


//Check for the extension command to be loaded
if(vkSomeFunctionEXT != NULL)
{
    //the vkSomeFunctionEXT Vulkan command is not null and callable
}

//If you want to unload all loaded pointers
vkewQuit();
```

# How to generate `vkew.h`

Make sure you have `python3` and `git` installed on your system, run the following:

```bash
git clone <this repository address> -- recursive
cd vkew
python3 gen.py 
```

To select the version of Vulkan the header is generated against, simply checkout the correct tag of the `Vulkan-Headers` submodule.

The recommended approach for that is to check the content of the `VK_HEADERS_VERSION` macro used in your project/Vulkan SDK installation, and find the tag in question. 

```bash
cd Vulkan-Headers
git checkout v1.2.203 # For example, the Android NDK shipped with header version == 203 at the time we're writing this.
cd ..
python ./gen.py
```

## Legal

`vkew.h` and the generator script Copyright (C) 2023 LIV Inc. Licensed under the MIT License Agreement

*Vulkan™ is a trademark owned by The Khronos Group Inc. and is registered as a trademark in China, the European Union, Japan and the United Kingdom.*

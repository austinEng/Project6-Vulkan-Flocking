Vulkan Flocking: compute and shading in one pipeline!
======================

**University of Pennsylvania, CIS 565: GPU Programming and Architecture, Project 6**

* Austin Eng
* Tested on: Windows 10, i7-4770K @ 3.50GHz 16GB, GTX 780 3072MB (Personal Computer)

## Vulkan Boids
![](vulkan_boids.gif)

This is a 2D port of my [CUDA flocking](https://github.com/austinEng/Project1-CUDA-Flocking) project over to Vulkan. 

Vulkan requires explicit descriptors for pipelines and commands so that it knows exactly what types of commands to expect. Since we declare everything, it doesn't have to dynamically allocate memory for commands. Vulkan can optimize if we preallocate the buffers we will use.

Multiple descriptor sets in a layout can be useful for ping-ponging buffers as we are doing in this flocking example. However, more generally, it can be used when two independent sets of data are needed in a one computation. For example, we may have a descriptor set for particle data and another for mesh data when computing particle-mesh collisions.

Vulkan also allows multiple command queues. However, one must be careful because commands may be pulled from these queues in an arbitrary order leading to problems if the intent was to execute commands sequentially. Furthermore, if a buffer is mutated by a command, then it may unexpectedly mutate if future commands were relying on old data.

Sharing data between compute and rendering pipelines allows for greater performance because all data stays on the GPU. We don't have to incur costs of slow memory transfers involved when pulling computed data from the GPU and then copying to it for rendering again.

### Credits

* [Vulkan examples and demos](https://github.com/SaschaWillems/Vulkan) by [@SaschaWillems](https://github.com/SaschaWillems)

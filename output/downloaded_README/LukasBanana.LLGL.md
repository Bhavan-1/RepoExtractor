[![Build status](https://ci.appveyor.com/api/projects/status/j09x8n07u3byfky0?svg=true)](https://ci.appveyor.com/project/LukasBanana/llgl)

Low Level Graphics Library (LLGL)
=================================

<p align="center"><img src="docu/LLGL_Logo.png"/></p>

License
-------

[3-Clause BSD License](https://github.com/LukasBanana/LLGL/blob/master/LICENSE.txt)


Documentation
-------------

- [Getting Started with LLGL](docu/GettingStarted/Getting%20Started%20with%20LLGL.pdf) (PDF)
with Introduction, Hello Triangle Tutorial, and Extensibility Example with [GLFW](http://www.glfw.org/)
- [LLGL Reference Manual](docu/refman.pdf) (PDF)
- [LLGL Coding Conventions](docu/CodingConventions/Coding%20Conventions%20for%20LLGL.pdf) (PDF)
- [Tutorials and Examples](tutorial) (Overview)


Progress
--------

* **Version**: 0.02 Beta (see [ChangeLog](docu/ChangeLog))

| Renderer | Progress | Remarks |
|----------|:--------:|---------|
| OpenGL | ~90% | |
| Direct3D 11 | ~85% | Depth-textures are incomplete |
| Direct3D 12 | ~15% | Experimental state; Tutorials working: 01, (02), (03), 06, 07, (10) |
| Vulkan | ~30% | Experimental state; Tutorials working: 01, 02, 03, 06, 07, 10 |

| Platform | Progress | Remarks |
|----------|:--------:|---------|
| Windows | 100% | Tested on *Windows 10* |
| Linux | 50% | Tested on *Kubuntu 16*; Anti-aliasing is currently not supported |
| macOS | 50% | Tested on *macOS Sierra*; Not all tutorials are running |
| iOS | 1% | Currently not compilable |


Thin Abstraction Layer
----------------------

```cpp
// Unified Interface:
CommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex);

// OpenGL Implementation:
void GLCommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    const GLsizeiptr indices = firstIndex * renderState_.indexBufferStride;
    glDrawElements(
        renderState_.drawMode,
        static_cast<GLsizei>(numIndices),
        renderState_.indexBufferDataType,
        reinterpret_cast<const GLvoid*>(indices)
    );
}

// Direct3D 11 Implementation
void D3D11CommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    context_->DrawIndexed(numIndices, firstIndex, 0);
}

// Direct3D 12 Implementation
void D3D12CommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    commandList_->DrawIndexedInstanced(numIndices, 1, firstIndex, 0, 0);
}

// Vulkan Implementation
void VKCommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    vkCmdDrawIndexed(commandBuffer_, numIndices, 1, firstIndex, 0, 0);
}
```



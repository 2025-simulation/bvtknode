# Learn and abstract the [official tutorial](https://bvtknodes.readthedocs.io/en/latest/)

## [A Gallery Thread on Blenderartists](https://blenderartists.org/t/bvtknodes-gallery/1161079)
**1. Todo**:

- [ ] 后期可以学习一下如何使用 blender 再借助 BVTKNodes 插件渲染 OpenFOAM 数据。这个可以不用管，知道有这个 wiki 就好。
- [ ] 观看教学视频，总结笔记。
- [ ] 对于瞬时数据的渲染还是有问题，那么现在解决了吗？
- [ ] 学习如何使用脚本控制节点工作流。
- [ ] 如何导入 `.vtk.series` 文件。

**2. Summary**：

> I’ve been thinking about creating a “Blender How-To for OpenFOAM users” to OpenFOAM wiki Blender page 30 or somewhere over there, but have not yet done this. Maybe one day…

这里是如何使用 Blender 处理 OpenFOAM 的建议网站。
[OpenFOAM wiki Blender page](http://openfoamwiki.net/index.php/Blender)

> Meanwhile, to learn Blender I suggest you go through tutorials in Youtube and Blender Cloud 2. To learn about BVTKNodes, the best material now is the Blender Conference 2018 BVTKNodes presentation 31 by Silvano and Lorenzo. After that you can try out some of the node setups shown in this thread. Beware: It is not as easy as Paraview. Also, I am still learning how to use VTK…

学习使用 BVTKNodes 的视频。
[Blender Conference 2018 BVTKNodes presentation](https://www.youtube.com/watch?v=KcF4LBTTyvk)

> Edit: I have not animated transient data with BVTKNodes. There is currently bug in Blender 2.8 3 which makes it necessary to use cumbersome workarounds for changing time steps.

还没有实现瞬态数据的渲染。（瞬态数据：随时间变化的数据）。
后面的回答似乎证明可以渲染动画，包含了单纯的镜头变化，还有数据也有变化。
[bug in Blender 2.8](https://developer.blender.org/T66392)

> New feature added: File series (e.g. file_0000.vtk, file_0001.vtk, …) can now be animated in BVTKNodes by adding Time Selector node immediately after appropriate Reader node (e.g. vtkPolyDataReader). When frame number is changed in Blender time line, the file name in reader node is updated accordingly.

这个的意思似乎是可以通过 `Time Selector` 就实现控制时间步，我们似乎不需要 `vtk.series` 文件。

> Here is a node tree example how to visualize points colored by velocity magnitude. Points were read in from .vtk file. vtkMaskPoints is used to decrease point count. The problem with this approach is that end result will have high vertex/poly count, because geometry is generated for individual points. If there are numerous points, it would be far more efficient to just pass points and vertex colors to Blender and then use Blender particle instancing to visualize points. That is not a feature yet in BVTKNodes, this idea goes to TODO list… However, as I see the potential here is huge for particle simulation visualizations, I’ll try to see to it next.

似乎作者正在对粒子数据进行优化处理。

> However, the simulation data which we are dealing with, are typically very large (tens of GB to TB) and it is not possible to load them in Blender. Do you think this could be overcome somehow (e.g., to replace the data with a proxy object)?

> Also, when I change some property in the BVTK pipeline, the whole calculation starts over from the beginning. Is it possible to skip some computationally expensive steps or at least abort ongoing calculation?

似乎 blender 处理过大数据会崩溃。

> FYI I’ve now added a simple cone creation and rendering example to the docs to show how to use Blender Python Scripting to drive BVTKNodes 14. The example is meant for those who want or need to script BVTKNodes.

可以使用脚本，而不是鼠标点击实现工作流，这也许对提升使用效率有帮助。
[how to use Blender Python Scripting to drive BVTKNodes](https://bvtknodes.readthedocs.io/en/latest/BVTKNodes.html#scripting-in-blender)

**3. Attention**：

1. blender 处理大量数据可能会崩溃。

## BVTKNodes Addon for Blender


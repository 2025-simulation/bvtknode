# BVTKNodes Addon for Blender

## Intro

convert VTK data into Blender objects.

at least to know Blender 3D Viewport, Node editor, Materials, Lighting and Rendnering basics,

learn Blender


To learn Blender, see resources at [blender.org](https://www.blender.org/)
, [Blender 2.8 fundamentals series in Youtube](https://www.youtube.com/playlist?list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6)
and search for Blender tutorials on a topic.

To learn VTK, see [VTK wiki](https://vtk.org/Wiki/VTK/Learning_VTK),
[the VTK Textbook](https://vtk.org/vtk-textbook/)
and view [VTK discourse forum](https://discourse.vtk.org/).

## Workspace Setup see [here]

To obtain a better experience of using blender, see
[workspace setup](https://bvtknodes.readthedocs.io/en/latest/BVTKNodes.html#workspace-setup)

`F3` to search nodes.

## To learn about blender

- moving of objects
- creation of background plane object for visualization
- setting up camera
- setting up lighting and world background
- modification of materials for objects
- modify settings for rendering engine
- rendering of image
- possibly composition and finally saving of image file

## Node Status

- Out-of-date (green): VTK level are not in sync.
- Updating (blue): VTK level is currently being updated.
- Up-to-date (dark gray): Node and VTK level are in sync.
- Upstream-changed (orange): Some value in an upstream node has been changed,
updated needed.
- Error (red): Something went wrong, execution has been stopped.

## Tabs in BVTK Node Editor

Tabs are located in the Sidebar of the BVTK Node Editor. You can hide
and view the Sidebar by pressing "N" key while hovering mouse over the
BVTK Node Editor.

Note: Some tabs become visible only after you select
a VTK node in the node tree. The properties and operations shown in tabs
will affect the active node.

**1. Item, Tool and View Tabs**

Just default Blender tabs, which show node properties, node tools and view.

**2. Properties**

- Show/Hide Properties: shows list of VTK object boolean properties,
  which can be hidden or shown in the node based on this setting.
  Values for hidden properties are ignored (not set to VTK objects
  during updates).
- Edit Custom Code: operator copies node's custom code into
  **BVTK** Text Block in `Text Editor`, where it is possible to add and
  edit Python code. The code will be run, line by line, for the VTK
  object represented by this node when the node is updated.
- Save Custom Code: operator saves the text from the BVTK Text Block
  into custom code storage string of the active node. Custom Code will be
  shown in the node (editor screen updates when mouse cursor enters it)
  if there is any saved to it.

**3. Inspect**

This tab contains global settings, tools for debugging and information.

- Inspect tab shows the add-on and VTK versions at the top.

- `Update Mode` determine when to when to update.
  - **No Automatic Updates** will not update automatically
  - **Update Current Automatically** will only update current node and
    upstream nodes.
  - **Update All Automatically** will update upstream nodes (if
    needed), the current node and downstream nodes automatically.

The following operators are available when a node is active:

> Not every node has this option

- **Update Node** operator will call a node specific update routine on
  the active node.
- **Documentation** will show doc string of the VTK object in the
  BVTK Text Block in the Text Editor.
- **Node Status** will show status of the VTK object in the
  BVTK Text Block in the Text Editor.
- **Output Status** will show status of the VTK object in the
  BVTK Text Block in the Text Editor.
- **Online Documentation** will open up web browser showing the
  Doxygen generated documentation for the very latest nightly
  version of VTK. Warning: Documentation may not exactly match
  the version of VTK used in BVTKNodes!

**4. Favorites**

This tab lists favorite nodes. You can delete and add nodes for easy
access here.

**5. Tree**

Node tree related operations.

- **Export JSON** exports the current node tree as JSON file.
  Please note that exported information includes full path names
  e.g. in VTK data reader nodes.
- **Import JSON** imports the current node tree as JSON file.
- **Arrange** will try to arrange node tree for a clean view.
  Warning: Does not work well for complex node trees.
  实际上并不好用。
- **Examples** contains a selection of example node trees you can
  try out.


## VTK Nodes

All node names that start with lower case text 'vtk' represent the
[VTK classes](https://vtk.org/doc/nightly/html/classes.html),
for example *vtkArrowSource*.
All other nodes are
[special nodes](https://bvtknodes.readthedocs.io/en/latest/BVTKNodes.html#special-nodes)
for BVTKNodes.

> Some VTK operators require *vtkPassArrays*, *vtkAssignAttribute* or other nodes to
> activate arrays to operate on to get correct result.
> See example in
> [Node Examples for Unstructured Grids](https://bvtknodes.readthedocs.io/en/latest/ug_nodes.html#ug-nodes)

## Addition of Custom Code to VTK Nodes

Many VTK nodes require special input from the user to work correclty.
You can activate a VTK node, use the **Online Documentation** of *Inspect* tab to learn.
The custom code is run in the end, so it will overwrite the setting.

Editing of Custom Code is done using Blender Text Editor:

- Select a VTK node in BVTK Node Tree
- In *Properties* Tab, run **Edit Custom Code**.
- Go to Blender Text Editor, and add/edit code in **BVTK** text block.
- To save edited text to active node, run **Save Custom Code** in
  *Properties* Tab. Updated code is shown on the node bottom when mouse
  cursor enters BVTK Node Tree area (see bottom example in
  [extract_boundary_surfaces](https://bvtknodes.readthedocs.io/en/latest/ug_nodes.html#extract-boundary-surfaces),
  *vtkOpenFoamReader* node)

There is also a *Custom Code* option at the bottom of every node.

## Customized VTK Nodes

Various VTK nodes have been customized to ease use in Blender
(see
[Customization of Node Python Code](https://bvtknodes.readthedocs.io/en/latest/BVTKNodes.html#customization-of-node-python-code)
):

<!-- #### vtkContourFilter -->

<!-- Contour values are specified in two fields: First value is input in -->
<!-- **Single Value** field, and the rest in the **Additional Values** -->
<!-- field, as a comma separated text string of values. The Single Value -->
<!-- field can be keyframed in Blender, to create an animation of the -->
<!-- changing value. -->

<!-- #### vtkPlane -->

<!-- This node specifies an infinite plane suitable for e.g. slicing 3D VTK -->
<!-- cell data (see example  -->
<!-- [cutting_field_data](https://bvtknodes.readthedocs.io/en/latest/ug_nodes.html#cutting-field-data). -->
<!-- Plane can be -->
<!-- specified by manual input of **Normal** and **Origin** vectors, or by -->
<!-- selecting an existing Blender Object (must be either a Plane or an -->
<!-- Empty Blender Object type) from the *Orientation Object* dropdown -->
<!-- menu. The location and rotation of the named Blender Object is used to -->
<!-- calculate Normal and Origin for *vtkPlane*. -->


## Special Nodes

### VTK To Blender Mesh

This is the new main node for exporting vertices, edges and boundary
faces directly from VTK objects into a Blender mesh object, without
need for any additional pre-processing nodes. Conversion is carried
out for all
[linear VTK cell types](https://lorensen.github.io/VTKExamples/site/VTKFileFormats/)
as well as [polyhedrons](https://vtk.org/Wiki/VTK/Polyhedron_Support).
The node contains same basic options as `VTK To Blender` node with
following additions:

- **Recalculate Normals**: This option will automatically compute and
  set "outward" normals for faces, regardless of original face normal
  directions.
- **Create All Verts**: If disabled, only boundary vertices (vertices
  part of boundary faces and edges) are created. If enabled, all
  vertices (including internal and unconnected vertices) are exported.
- **Create Edges**: If enabled, exports also wires (edges that are not
  part of any face).
- **Create Faces**: If enabled, creates boundary faces (faces used by
  only one VTK cell). Internal faces (faces shared by two
  3D cells) are not exported.
- **Force Update Upstream**: This operator will force an update on the
  upstream nodes and this node. This was added for special cases where
  the update system does not detect a possible need for running an
  update.
- **Motion Blur**: Boolean option to enable mesh motion blur. If
  enabled, the following options become available:
- **Motion Blur By** specifies name of a point vector field (3 value
  components) which is to be used for creating pointwise motion
  for the mesh. The naming convention is the same used in *Color
  Mapper* Node. E.g. value "P_velocity" means that the point vector
  field name to be applied is "velocity".
- **Time Step for Motion Blur** specifies the time difference between
  two frames. It is used for calculating the length scale of motion blur.

Blender's Motion Blur settings are located in the Render Properties
Panel. The *Position* is set to *Start on Frame* to get correct
blur for rendering an animation. A still example of motion blur is
available in the example node tree *cubeflow_vector_glyphs*. You need
to enable *Motion Blur* in the *Blender To VTK Mesh* Node.

### VTK To Blender Image

This node converts VTK Image Data (*vtkImageData*) into a Blender
Image, viewable in Blender Image Editor. The node requires two
options:

- **Image Name** is the name shown for the picture in Blender
  Image Editor.
- **Field Name** specifies the VTK field name, values from which are
  used for the image.
- **Tip:** You may use e.g. *vtkResampleToImage* to convert planar data into
VTK image data, see example node tree *cubeflow_cut_plane_to_image*.


<!-- #### VTK To Blender Particles -->

<!-- > This node is experimental and unreliable -->
<!-- > see issue [here](https://github.com/tkeskita/BVtkNodes/issues/12) -->

<!-- This node converts VTK point data into Blender particle object instancing -->
<!-- to presente points with a mesh object and take little memory. -->

<!-- - **Glyph Name** specifiy the glyph object. It should be 1 m in length, -->
<!--   and point to positive X axis. -->
<!-- - **Direction Vector Array Name** (optional): Name of a VTK vector -->
<!--   data array, with which the glyph object will be aligned at point -->
<!--   locations. -->
<!-- - **Scale Value or Name** (optional): A constant multiplier value or -->
<!--   name of a VTK scalar array used to scale the glyph object at point -->
<!--   locations. -->
<!-- - **Color Value Array Name** (optional): Name of a VTK scalar array of -->
<!--   ramp values that will be used for coloring the object at point -->
<!--   locations. Color ramp values are available via `Particle Info node -->
<!--   <https://docs.blender.org/manual/en/latest/render/shader_nodes/input/particle_info.html>`_'s -->
<!--   *lifetime* output (until a better access becomes possible). -->
<!-- - **Particle Count** specifies the maximum number of particles which -->
<!--   will be converted into the Particle System. -->
<!-- - **Generate Material** will generate a default colored diffuse -->
<!--   material which will be used for glyph object at particle locations. -->
<!-- - **Initialize** operator will initialize the Blender Particle System -->
<!--   with the number of particles specified in *Particle Count*. This -->
<!--   operator must be run before node pipeline is updated. -->
<!-- - **Update Node** updates the node pipeline connected to this node. -->

<!-- **Usage**: First, create a glyph object. Then input the data in node -->
<!-- fields, and run **Initialize**. After that, every run of Update Node -->
<!-- updates the particle data. Note: -->

<!-- - Running Update Node after changing frame number in Blender Timeline -->
<!--   is required to update particle data correctly. -->
<!-- - Particles may not show up updated in the 3D Viewport after -->
<!--   frame change, but they should be still rendered correctly. -->
<!--   Left-clicking on 3D viewport should update the view. -->
<!-- - Particle colors show up correctly only in Rendered Viewport Shading -->
<!--   mode, and only using Cycles Render Engine. -->
<!-- - It is not possible to modify particles in Blender. You need to do -->
<!--   all modifications on VTK side prior to using this node. -->

<!-- The example tree *cubeflow_particle_instancing* illustrates the usage -->
<!-- of this node: -->

<!-- - Run **Update Node** on *VTK To Blender Mesh* node. -->
<!-- - Run **Initialize** on *VTK To Blender Particles* node. -->
<!-- - Run **Update Node** on *VTK To Blender Particles* node. -->
<!-- - Left-click on 3D viewport to force update of the view. -->
<!-- - Change the Render Engine to Cycles. -->
<!-- - Render Image to see results (with correct colors). -->

<!-- .. _VTKToBlenderVolume: -->

<!-- #### VTK To Blender Volume -->

<!-- This node converts 3D VTK image data (*vtkImageData*) into OpenVDB -->
<!-- grids. The VDB data is then automatically imported into Blender as a -->
<!-- Volume Object, ready to be used in volumetric rendering using the -->
<!-- *Principled Volume Shader*.  This node requires `pyopenvdb` in -->
<!-- Blender, now available in Blender version 3.6 and later. -->

<!-- Please see VTK To OpenVDB Exporter below for description of field names. -->

<!-- .. _VTKToOpenVDBExporter: -->

<!-- #### VTK To OpenVDB Exporter -->

<!-- This node exports selected 3D *vtkImageData* arrays (density, color, -->
<!-- flame and temperature inputs) into a JSON file, which can be then -->
<!-- converted into OpenVDB (.vdb) file format using an external -->
<!-- installation of *pyopenvdb*. OpenVDB files can be then imported back -->
<!-- to Blender as a Volume Object for volumetric rendering, using e.g. the -->
<!-- *Principled Volume Shader*. -->

<!-- - **Name** is the base name of the OpenVDB file to be created. -->
<!-- - **Density Field Name** specifies the field name of scalar array to -->
<!--   be used for the *Density* output of Volume Info node in Blender -->
<!--   Shader Editor. -->
<!-- - **Color Field Name** is used for 3D vector array as *Color* output -->
<!--   in Volume Info node. -->
<!-- - **Flame Field Name** is scalar field exposed as *Flame* output in -->
<!--   Volume Info node. It can be used for specifying e.g. emission -->
<!--   strength. -->
<!-- - **Temperature Field Name** is a scalar field shown as *Temperature* -->
<!--   output in Volume Info node. -->

<!-- Upon running **Update Node**, the node creates a file like -->
<!-- ``volume_00001.json`` (format is name + frame number) into the folder -->
<!-- where the blender file is saved.  If node input is not a data suitable -->
<!-- for exporting (VTK 3D Image Data or Structured Points Data), the node -->
<!-- shows an error message, otherwise data dimensions are shown. -->

<!-- To convert JSON file to OpenVDB, the user must run a Python script -->
<!-- ``convert_to_vdb.py`` located in the add-on source directory -->
<!-- *utils*. You can also `download script directly from github -->
<!-- <https://raw.githubusercontent.com/tkeskita/BVtkNodes/master/utils/convert_to_vdb.py>`_. -->
<!-- Example usage of command:: -->

<!--   python3 convert_to_vdb.py volume_00001.json -->

<!-- .. note:: -->

<!--    If you receive error like: -->
<!--        "libjemalloc.so.2: cannot allocate memory in static TLS block" -->
<!--    then prepend command with *LD_PRELOAD* with correct path to *libjemalloc.so.2*, e.g.: -->
<!--        ``LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so.2 python3 convert_to_vdb.py volume_00001.json`` -->

<!-- Running *convert_to_vdb.py* requires that *pyopenvdb* module is -->
<!-- available to Python. *pyopenvdb* can be provided externally, depending -->
<!-- on your system: -->

<!-- * **Ubuntu Linux** : install system package: -->
<!--   ``sudo apt-get install python3-openvdb`` -->
<!-- * **Windows**: ??? -->

<!-- If you find out free packages that provide *pyopenvdb*, -->
<!-- `please comment here <https://github.com/tkeskita/BVtkNodes/issues/25>`_. -->

<!-- See also `other alternative routes from VTK to OpenVDB <https://discourse.vtk.org/t/vtk-to-openvdb-file-format/6322>`_. -->

<!-- **Hint**: Add Math or Vector Math nodes in the Shader Editor to modify -->
<!-- array values to obtain wanted visual results, instead of adding the -->
<!-- mathematical manipulation of the arrays in BVTKNodes. See -->
<!-- :ref:`volumetric_rendering` example. -->

<!-- VTKImageData Object Source -->
<!-- ^^^^^^^^^^^^^^^^^^^^^^^^^^ -->

<!-- This node creates an empty 3D VTK image data (*vtkImageData*) object. -->

<!-- - **Origin** is the origin coordinates of the image data. -->
<!-- - **Dimensions** set the number of voxels in each primary axis. -->
<!-- - **Spacing** specify voxel side lengths in the three axes. -->
<!-- - **Multiplier** scales both all *Dimensions* and all *Spacing* values -->
<!--   while (approximately) retaining image bounding box size. -->

<!-- .. _info-node: -->

### Info

It will show what the current VTK pipeline contains.

- Type of VTK data.
- Number of points and cells in VTK data.
  *Note:* "cell" in VTK terminology can refer to a face or a 3D cell.
- X, Y and Z coordinate ranges of the data.
- Point and cell data (with names, type and value ranges)

### Color Mapper

You will see the colors in Blender 3D Viewport
when Shading Mode is set to either **Material Preview**
or **Rendered**.

- **lookuptable** connector must be connected to a *Color Ramp* node
- **Generate Scalar Bar** generate a color legend object to the
  Blender scene. Warning: This feature is not working well.
- **Color By** specific the array to add colors.
  Remember to add prefix to the array to ensure the array type
  ("C_" for cell/face values, or "P_" for point values)
  If the array is a vector array,
  then magnitude of the vector is used for the color scale.
- **Auto Range** will update the value range for the data array
  specified in *Color By* automatically during update, if enabled.
- **min** and **max** specify the value range (if *Auto Range* is disabled).
- **output** connector should be attached to a *VTK To Blender Mesh* node.

### Multi Block Leaf

This node allows you to filter to a single data set
, when the input is of type *vtkMultiBlockDataSet*.
**Block Name** text field specifies the data set name.
It may need to use twice to specify a data set

### Time Selector

This node can be connected immediately after a VTK reader node.

- **Use Scene Time** directly controlle via the Blender Timeline Editor.
  The **Time Index** in the Time Selector node is
  automatically updated with timeline.

- If **Use Scene Time** time is disabled, then it is possible to use
  `Global Time Keeper` node to animate the `Time Index` value (see
  below).

- If the VTK Reader is not aware of time data, and if File Name of the
  Reader node contains integers at the end of the File Name,
  then the integer part of the File Name is updated to match the file name
  corresponding to the Timeline frame number.

  The file name matching with the frame number is made as follows:
  A file list is generated from files in the data directory, which
  follow the same file naming convention (file name characters +
  integer number + extension) as the current File Name.
  Then the list is sorted by the integer number part, and the file name
  matching the (modulo of the) frame number is selected.
  Data files are looped continuously
  when frame number exceeds number of data files.
  The integer number part can be arbitrary
  (not necessarily a continuous sequence of numbers).

## Python Interaction and Custom Filter

It is possible to interact with nodes and live VTK objects via
Blender's Python Console. Python Console includes three help operators
for BVTKNodes:

* *Get Node* operator inserts text which returns access to active
  node.
* *Get VTK Object* inserts command which returns access to VTK object
  of the active node.
* *Get Node Output* inserts text which returns the Output of VTK
  object.

[customeFilter](../static/images/customFileter.png)
*Custom Filter* node allows user to write Python code in Blender Text Block.
Click the magnifying glass icon will create a new file in the Text Editor,
then click the book icon nearby, allow you to choose any files you write
in the Text Editor.
Finally you can choose any function defined in the file you choosed in the
Function bar.

Here is an example of a *Custom Filter* which calls
*vtkThreshold* with custom parameter values::
```python
  def myThreshold(input_obj):
    vtkobj = vtk.vtkThreshold()
    vtkobj.SetInputData(input_obj)
    attr_name = "p"  # Array name for thresholding
    attr_type = vtk.vtkDataObject.FIELD_ASSOCIATION_CELLS
    value1 = float("0.01")  # min value
    value2 = float("0.02")  # max value
    vtkobj.ThresholdBetween(value1, value2)
    vtkobj.SetInputArrayToProcess(0, 0, 0, attr_type, attr_name)
    vtkobj.Update()
    return vtkobj.GetOutput()
```
Learn VTK [here](https://vtk.org/doc/nightly/html/)

## Scripting in Blender

You can use a Python script to create nodes, change node values,
link the nodes and run updates. Copy-paste the following code to a
Text Block in *Text Editor* and Run Script to create `image.png` 
render of a cone. 

You can enable *Python Tooltips* in Edit -> Preferences -> 
Interface -> Display -> Tooltips to see variable name when
hovering over a node setting in node tree.

```python
  # BVTKNodes Blender Python Scripting Example
  import bpy

  node_tree = bpy.data.node_groups.new("BVTKNodeTree", type="BVTK_NodeTreeType")
  nodes = bpy.data.node_groups["BVTKNodeTree"].nodes
  links = bpy.data.node_groups["BVTKNodeTree"].links

  # Create nodes
  cone = nodes.new(type="VTKConeSourceType")

  cone.m_Height = 3.0
  cone.m_Radius = 1.5
  elevation = nodes.new(type="VTKElevationFilterType")
  mapper = nodes.new(type="BVTK_Node_ColorMapperType")
  mapper.color_by = "P_Elevation"
  ramp = nodes.new(type="BVTK_Node_ColorRampType")
  vtk_to_blender = nodes.new(type="BVTK_Node_VTKToBlenderMeshType")
  vtk_to_blender.m_Name = "cone"
  vtk_to_blender.generate_material = True

  # Link nodes
  links.new(cone.outputs["output"], elevation.inputs["input"])
  links.new(elevation.outputs["output"], mapper.inputs["input"])
  links.new(ramp.outputs["lookupTable"], mapper.inputs["lookuptable"])
  links.new(mapper.outputs["output"], vtk_to_blender.inputs["input"])

  # Update from the final node
  vtk_to_blender.update_vtk()

  # Print out information
  ob = bpy.data.objects["cone"]
  print ("Mesh has %d vertices" % len(ob.data.vertices))
  print ("Mesh has %d faces" % len(ob.data.polygons))

  # Add camera
  camera_data = bpy.data.cameras.new("Camera 1")
  camera_object = bpy.data.objects.new("Camera 1", camera_data)
  camera_object.location = (10, -10, 10)
  camera_object.rotation_euler = (1.0, 0, 0.8)  # radians
  bpy.context.scene.collection.objects.link(camera_object)
  bpy.context.scene.camera = camera_object

  # Add light
  light_data = bpy.data.lights.new(name="Light 1", type="POINT")
  light_data.energy = 5000
  light_object = bpy.data.objects.new(name="Light 1", object_data=light_data)
  light_object.location = (10, 5, 10)
  bpy.context.collection.objects.link(light_object)

  # Update scene, if needed
  dg = bpy.context.evaluated_depsgraph_get()
  dg.update()

  # Render an image
  bpy.context.scene.render.filepath = "image.png"
  bpy.ops.render.render(write_still = True)
```


## Customization of Node Python Code

If an automatically generated node does not provide good
functionality, it is possible to override the autogenerated node code
with custom Python code. 
Please feel free to submit such node code customizations at
[github issues page](https://github.com/tkeskita/BVtkNodes/issues)

## Information and Error Messages

Nodes show messages at the UI message box at node top, if any text is
available. In addition, node is shown in red color if an error is
encountered. Unfortunately, VTK level error messages are not currently
captured to this message, so you may need to see debugging messages
(see below) when trying to find out cause for a failure.


## Debug Messages

Please use *Info* node for viewing pipeline contents. 

BVTKNodes additionally uses Python Logging module, which prints out
debug messages to the terminal where Blender is started, but only when
Python Logging is configured properly (see Configuring Logging chapter
in [Logging from Python code in Blender
](https://code.blender.org/2016/05/logging-from-python-code-in-blender/)
To see the debug messages (on Linux in this example), you can create
a text file `$HOME/.config/blender/{version}/scripts/startup/
setup_logging.py` with contents

```python
  import logging
  logging.basicConfig(format='%(funcName)s: %(message)s', level=logging.DEBUG)
```

## Special Use Cases

See [Node Examples for Unstructured Grids](https://
bvtknodes.readthedocs.io/en/latest/ug_nodes.html#ug-nodes).

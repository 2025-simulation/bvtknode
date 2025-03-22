## The Official Tutorial

1. `Shift+F3` twice: open the layout and create a new one.
The old one is the official template, so we can not find the node about vtk. 
2. `Shift+A` to add a new node. 
The official tutorial provide a vti file. 
you can get from [here](./data/head.vti)

### The node procedure

- vtkXMLImageDataReader
  - vtkImageGaussianSmooth
    - vtkContourFilter: Single Value=66
      - VTK To Blender Mesh: Name=skel; checkout Smooth
    - vtkContourFilter: Single Value: 20
      - VTK To Blender Mesh: Name=skin; ckeckout Smooth

# How to render the OpenFOAM data 

1. A openFOAM reader is request
2. if you want to choose one part of the data. Two `Multi Block leaf` is needed. 

I think it must separated to vtk and FOAM data, and the vtk data seem to store in the dem, 
and the FOAM just to call the vtk data, remember the vtk is divided into 2 part, too. 

The mesh data and other
point and cell


There is many data in the vtk, but foam convert it into different files it make hard to read.
So we need to convert the data into the vtk with `foamToVTK`

first install openFOAM
[openFOAM](https://develop.openfoam.com/Development/openfoam/-/wikis/precompiled/debian)

```shell
source /usr/lib/openfoam/openfoam2412/etc/bashrc
```

or you can add the code to the file of `.zshrc` or `.bashrc`. 
CoutorFilter


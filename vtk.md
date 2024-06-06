
## Install

```
cd src
git clone --recursive https://gitlab.kitware.com/vtk/vtk.git
cd VTK
```
```
# https://github.com/lorensen/PoissonReconstruction/blob/master/PoissonReconstruction.remote.cmake
# Download
PoissonReconstruction.remote.cmake
# Add to VTK/Remote
```
```
mkdir build
cd build

cmake-gui

CMAKE_BUILD_TYPE Release

Add Entry
Module_PoissonReconstruction 

VTK_BUILD_EXAMPLES

>> Configure, Generate

make -j
sudo make install
```

## Examples
```
[Examples](https://examples.vtk.org/site/Cxx/)
```


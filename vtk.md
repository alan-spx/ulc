
## Install

```
cd src
git clone --recursive https://github.com/Kitware/VTK.git
cd VTK
git co v9.0.0
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
https://examples.vtk.org/site/Cxx
```


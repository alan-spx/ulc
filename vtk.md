
## Install

```
cd src
git clone https://github.com/Kitware/VTK.git
cd VTK
git co v9.0.0
git co v8.1.1
```
```
mkdir build
cd build

cmake-gui

# https://discourse.vtk.org/t/poissonreconstruction/4777
# Check **Grouped** and **Advanced** boxes
# Check **VTK** session

VTK_MODULE_ENABLE_VTK_PoissonReconstruction
# Then set the values to WANT then configure and build.

CMAKE_BUILD_TYPE Release

VTK_BUILD_EXAMPLES

>> Configure, Generate

make -j
sudo make install
```

## Examples

[Examples](https://examples.vtk.org/site/Cxx)


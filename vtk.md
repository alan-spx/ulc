
## Install
[Github](https://github.com/Kitware/VTK.git)
```
cd src
git clone https://github.com/Kitware/VTK.git
cd VTK
git co v9.0.0
```
```
mkdir build
cd build

cmake-gui

# https://discourse.vtk.org/t/poissonreconstruction/4777
# Check **Grouped** and **Advanced** boxes

Module_PoissonReconstruction

CMAKE_BUILD_TYPE Release

>> Configure, Generate

make -j
sudo make install
```

## Examples

[Examples](https://examples.vtk.org/site/Cxx)



## Install

```
cd src
git clone --recursive https://github.com/Kitware/VTK.git
cd VTK
git co v9.0.0
```
```
mkdir build
cd build

cmake-gui

# Check **Grouped** and **Advanced** boxes
# Check **VTK** session

CMAKE_BUILD_TYPE Release

VTK_BUILD_EXAMPLES

>> Configure, Generate

make -j
sudo make install
```

## Examples
```
https://examples.vtk.org/site/Cxx
```


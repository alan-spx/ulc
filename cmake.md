## Basic C++11

```
cmake_minimum_required(VERSION 2.8)
project(person LANGUAGES C CXX)
set (CMAKE_CXX_STANDARD 11)

add_executable(person src/cout_sequence.cpp)
```

## OpenCV

```
cmake_minimum_required(VERSION 2.8)
project(bcali LANGUAGES C CXX)
set (CMAKE_CXX_STANDARD 11)

find_package(OpenCV 3.0.0 REQUIRED)
find_package(Eigen3 REQUIRED)

include_directories(EIGEN3_INCLUDE_DIR PATHS /usr/local/include/eigen3)

add_executable(bcali src/main.cpp 
		     src/calibrate.cpp
		     src/find_grids.cpp)
target_link_libraries(bcali ${OpenCV_LIBRARIES})
```

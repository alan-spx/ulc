## LORD-MicroStrain/microstrain_inertial

[Website](https://www.microstrain.com/inertial-sensors/3dm-gx5-25)  
[GitHub](https://github.com/LORD-MicroStrain/microstrain_inertial)

```
sudo apt install -y libgeographic-dev

git clone --recursive --branch ros https://github.com/LORD-MicroStrain/microstrain_inertial.git ~/catkin_ws/src/microstrain_inertial
rosdep install --from-paths ~/catkin_ws/src -i -r -y

cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash

```

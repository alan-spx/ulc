## LORD-MicroStrain/microstrain_inertial

[Website](https://www.microstrain.com/inertial-sensors/3dm-gx5-25)  
[GitHub](https://github.com/LORD-MicroStrain/microstrain_inertial)

## Install

```
sudo apt install -y libgeographic-dev

git clone --recursive --branch ros https://github.com/LORD-MicroStrain/microstrain_inertial.git ~/catkin_ws/src/microstrain_inertial
rosdep install --from-paths ~/catkin_ws/src -i -r -y

cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash

# Download udev.txt from
# https://github.com/LORD-MicroStrain/microstrain_inertial/blob/ros/microstrain_inertial_driver/debian/udev
sudo mv ~/Downloads/udev.txt /etc/udev/rules.d/100-microstrain.rules


```

## Run

```
roslaunch microstrain_inertial_driver microstrain.launch
```

## Check
```
rqt_plot /imu/data/linear_acceleration/x

rqt_plot /robot_pose_ekf/odom_combined/Pose/Point/x
rqt_plot /robot_pose_ekf/odom_combined/Pose/Quaternion/x
```

## robot_pose_ekf
[Website](https://wiki.ros.org/robot_pose_ekf)  
```

```

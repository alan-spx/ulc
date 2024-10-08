## LORD-MicroStrain/microstrain_inertial

[Website](https://www.microstrain.com/inertial-sensors/3dm-gx5-25)  
[GitHub](https://github.com/LORD-MicroStrain/microstrain_inertial)

## IMU memo
```
roslaunch microstrain_inertial_driver microstrain.launch

rosbag record /imu/data -o imu

python live_capture_timestamp.py 

rostopic echo -b imudata_2024-06-21-14-24-11.bag -p /imu/data > 2024-06-21-14-24-11.csv
```
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
# /home/alan/catkin_ws/src/microstrain_inertial/microstrain_inertial_driver/launch/microstrain.launch
    <remap from="/imu/data" to="/imu_data" />
```
```
# /opt/ros/noetic/share/robot_pose_ekf/robot_pose_ekf.launch
  <param name="odom_used" value="false"/>
  <param name="imu_used" value="true"/>
  <param name="vo_used" value="false"/>
```
```
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 imu_link odom_combined 10
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 imu_link base_footprint 10
```
```
roslaunch microstrain_inertial_driver microstrain.launch
```

## robot_pose_ekf

[Website](https://wiki.ros.org/robot_pose_ekf)  
<!--- 
```
rosdep install robot_pose_ekf
roscd robot_pose_ekf
rosmake

roslaunch robot_pose_ekf.launch

rqt_plot /imu/data/linear_acceleration/x

rqt_plot /robot_pose_ekf/odom_combined/Pose/Point/x
rqt_plot /robot_pose_ekf/odom_combined/Pose/Quaternion/x
```

```
sudo apt install -y ros-noetic-geographic-msgs 
cd catkin_ws/src
git clone https://github.com/norsechurros/Ekf-Fusion.git
cd ..
catkin_make
```
-->

## Check
```
rostopic echo /imu/data 
```

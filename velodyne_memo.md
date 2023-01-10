
```
roslaunch velodyne_pointcloud VLP16_points.launch
rosrun rviz rviz -f velodyne
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map velodyne 10

rosbag record -a
```


```
roslaunch velodyne_pointcloud VLP16_dual.launch
rviz rviz
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map vlp201 10
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map vlp202 10
```

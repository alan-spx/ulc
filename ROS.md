# ROS

## rosbag
```
rosbag record -a
rosbag play *.bag
rosbag play *.bag -r 5  // speed up 5X
rosbag info *.bag
rosbag record -O subset /topic1 /topic2
rosbag play subset.bag /horizontal_laser_3d:=/velodyne_cloud_3 /imu:=/imu/data     // play /hori... as /velo…
                    // from:=to
rosbag play -l name.bag  // loop
```

## rostopic
```
rostopic type /imu
rostopic list -v
rostopic info /horizontal_laser_2d 
rostopic echo /imu
rostopic pub [topic] [msg_type] [args]
rostopic list -v | grep sensor_msgs/LaserScan

/scan   type: sensor_msgs/LaserScan
        info: type, Publishers, Subscribers

rostopic pub -r 10 /cmd_vel geometry_msgs/Twist  '{linear:  {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 0.0}}'

rostopic hz /stereo_convert/left/image_raw

rostopic echo -b file.bag -p /topic > data.txt   // extract odometry
rostopic echo -b 200725_3.bag -p /odom > data.txt

rostopic echo /velodyne_points | grep frame_id
```

## ROS time to std::string
```
std::to_string(ros::Time::now().toSec()) + ".jpg"
```

## image_view
```
rosrun image_view image_view image:=/raw_image 
rosrun image_view extract_images _sec_per_frame:=0.01 image:=/raw_image 
```

## rqt
### - Plot
```
Plugins > Visualization > Plot
Topic > +(Add) > Select topic and drag to plot window
```

## 	plotjuggler
[Website](https://index.ros.org/p/plotjuggler/)  
```
sudo snap install plotjuggler-ros
```

##

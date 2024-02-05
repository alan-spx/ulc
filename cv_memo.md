## image_view
```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_front cam_serial:=#38810011

cd
rosrun image_view image_view image:=/cam_front_publish/image_rect

roslaunch tcam_extrinsic_calibration tcam_extrinsic_calibration.launch cam_name:=cam_front cam_serial:=#38810011
```

## PCL
```
sudo apt install pcl-tools
```

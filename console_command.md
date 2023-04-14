
```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_back cam_serial:=#38810018
roslaunch apriltag_localization apriltag_localization.launch cam_name:=cam_back cam_serial:=#38810018 show_image:=true
```

```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_back cam_serial:=#38810018
roslaunch cross_localization cross_localization.launch cam_name:=cam_back cam_serial:=#38810018 show_image:=true
```

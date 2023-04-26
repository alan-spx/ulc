
```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_front cam_serial:=#38810018
roslaunch apriltag_localization apriltag_localization.launch cam_name:=cam_front show_image:=true cam_serial:=#38810018
```

```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_front cam_serial:=#38810018
roslaunch cross_localization cross_localization.launch cam_name:=cam_front show_image:=true cam_serial:=#38810018 
```

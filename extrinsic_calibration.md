## Check

Make sure spike parameter is loaded.

## Go to home folder

```
cd  
```

## Run camera

```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_front cam_serial:=#38810018
```

## View image

```
rosrun image_view image_view image:=/cam_front_publish/image_rect  
```
click to save image

## Run calibration

**Run**

```
roslaunch tcam_extrinsic_calibration tcam_extrinsic_calibration.launch cam_name:=cam_front cam_serial:=#38810018  
```

**calibration_input.txt format**

x, y, z, u, v  
x, y, z, u, v  
x, y, z, u, v  
x, y, z, u, v  

**Result**

pose_robot_cam.yml

## Test  

**Copy file**

pose_robot_cam.yml --> pose_robot_cam_front.yml

**Run**

```
roslaunch apriltag_localization apriltag_localization.launch cam_name:=cam_front show_image:=true cam_serial:=#38810018  
```



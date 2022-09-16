**Check**

Make sure spike parameter is loaded.

**Go to home folder**

cd  

**Run camera**

roslaunch tcam_publish tcam_publish.launch cam_name:=cam_front cam_serial:=#38810017

**View image**

rosrun image_view image_view image:=/cam_front_publish/image_rect  
click to save image

**Run calibration**

roslaunch tcam_extrinsic_calibration tcam_extrinsic_calibration.launch cam_name:=cam_front cam_serial:=#38810017  


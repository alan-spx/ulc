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

## usb_cam  

```
sudo apt install ros-melodic-usb-cam
roslaunch usb_cam usb_cam-test.launch image_width:=1280 image_height:=960  
```


## velodyne_memo

```
roslaunch velodyne_pointcloud VLP16_points.launch
rosrun rviz rviz -f velodyne
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map velodyne 10

rosbag record -a




roslaunch velodyne_pointcloud VLP16_dual.launch
rviz rviz
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map vlp201 10
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map vlp202 10
```


## install_solar_cv

```
F10 -> UEFI

power never

sudo apt update
sudo apt install ssh geany pcmanfm net-tools

# scp install_mmpose ZscalerRootCerts.zip sol@10.60.1.119:

cd ZscalerRootCerts
sudo mkdir /usr/local/share/ca-certificates/extra
sudo cp ZscalerRootCertificate-2048-SHA256.crt /usr/local/share/ca-certificates/extra/root.cert.crt
sudo update-ca-certificates 
cd

wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb

Chrome settings:
Security
Manage certificates
Authorities
Import

Apriltag
git clone https://github.com/AprilRobotics/apriltag
cd apriltag
mkdir build
cd build
cmake ..
make -j
sudo make install

TIS
git clone https://github.com/TheImagingSource/tiscamera
cd tiscamera
./scripts/dependency-manager install
mkdir build
cd build
cmake -DBUILD_ARAVIS=ON ..
make -j
sudo make install

Set static IP

ROS
http://wiki.ros.org/melodic/Installation/Ubuntu

mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```


## NERF

```
pip install -r requirements.txt
sudo apt install python-pip
pip install -r requirements.txt
sudo apt install python3.7
pip install -r requirements.txt
sudo apt install python3-pip
pip3 install -r requirements.txt
python3.7 -m pip install scikit-build  
pip3 install -r requirements.txt
python3.7 -m pip install pip  
pip3 -V  
python3.7 -m pip install --upgrade pip    
python3.7 -m pip install -r requirements.txt  
python run_nerf.py --config configs/st3d.txt  
history
```


# 3D Object Pose Estimation - ROS - Realsense d435

![](https://github.com/yehengchen/dope_ros_realsense/blob/master/dope/dope_1.gif)
<img src="https://github.com/yehengchen/dope_ros_realsense/blob/master/dope/dope_2.png" width="60%" height="60%">

## DOPE Installing

__Step 1: Download the DOPE code__

    cd ~/catkin_ws/src
    git clone https://github.com/yehengchen/dope_ros_realsense.git

__Step 2: Install python dependencies__

    cd ~/catkin_ws/src/dope
    pip install -r requirements.txt

__Step 3: Install ROS dependencies__

    cd ~/catkin_ws
    rosdep install --from-paths src -i --rosdistro kinetic
    sudo apt-get install ros-kinetic-rosbash ros-kinetic-ros-comm
    Build

    cd ~/catkin_ws
    catkin_make

__Step 4: Download [the weights](https://drive.google.com/open?id=1DfoA3m_Bm0fW8tOWXGVxi4ETlLEAgmcg) and save them to the `weights` folder, *i.e.*, `~/catkin_ws/src/dope/weights/`.__

***

## ROS Wrapper for Intel® RealSense™ Devices

__Step 1: Install the latest Intel® RealSense™ SDK 2.0__

Install from [Debian Package](https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md#installing-the-packages) - In that case treat yourself as a developer. Make sure you follow the instructions to also install librealsense2-dev and librealsense-dkms packages.
OR
Build from sources by downloading the latest Intel® RealSense™ SDK 2.0 and follow the instructions under [Linux Installation](https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md)

__Step 2: Install the ROS distribution__
Install ROS Kinetic, on Ubuntu 16.04

__Step 3: Install Intel® RealSense™ ROS from Sources__
  
    cd ~/catkin_ws/src/

Clone the latest Intel® RealSense™ ROS from [here](https://github.com/IntelRealSense/realsense-ros/releases) into 'catkin_ws/src/'

    git clone https://github.com/IntelRealSense/realsense-ros.git
    cd realsense-ros/
    git checkout `git tag | sort -V | grep -P "^\d+\.\d+\.\d+" | tail -1`
    cd ..

Make sure all dependent packages are installed. You can check .travis.yml file for reference.
Specifically, make sure that the ros package ddynamic_reconfigure is installed. If ddynamic_reconfigure cannot be installed using APT, you may clone it into your workspace 'catkin_ws/src/' from [here](https://github.com/pal-robotics/ddynamic_reconfigure/tree/kinetic-devel) (Version 0.2.0)

    catkin_init_workspace
    cd ..
    catkin_make clean
    catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release
    catkin_make install
    echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    
***
## Running

__1. Start ROS master__
    ```
    cd ~/catkin_ws
    source devel/setup.bash
    roscore
    ```

__2. Start camera node (or start your own camera node)__
    
Realsense D435 & usb_cam node (./dope/config/config_pose.yaml):    
    ``` 
    topic_camera: "/camera/color/image_raw"            #"/usb_cam/image_raw"
    topic_camera_info: "/camera/color/camera_info"     #"/usb_cam/camera_info"
    ``` 
Start camera node:
    ``` 
    roslaunch realsense2_camera rs_rgbd.launch  # Publishes RGB images to `/camera/color/image_raw`
    ```

__3. Start DOPE node__
    ```
    roslaunch dope dope.launch [config:=/path/to/my_config.yaml]  # Config file is optional; default is `config_pose.yaml`
    ```

__4. Start rviz node__
    ```
    rosrun rviz rviz
    ```

## Debugging

* The following ROS topics are published (assuming `topic_publishing == 'dope'`):
    ```
    /dope/webcam_rgb_raw       # RGB images from camera
    /dope/dimension_[obj_name] # dimensions of object
    /dope/pose_[obj_name]      # timestamped pose of object
    /dope/rgb_points           # RGB images with detected cuboids overlaid
    /dope/detected_objects     # vision_msgs/Detection3DArray of all detected objects
    /dope/markers              # RViz visualization markers for all objects
    ```
    *Note:* `[obj_name]` is in {cracker, gelatin, meat, mustard, soup, sugar}

* To debug in RViz, run `rviz`, then add one or more of the following displays:
    * `Add > Image` to view the raw RGB image or the image with cuboids overlaid
    * `Add > Pose` to view the object coordinate frame in 3D.
    * `Add > MarkerArray` to view the cuboids, meshes etc. in 3D.
    * `Add > Camera` to view the RGB Image with the poses and markers from above.
    

## Citating

If you use this tool in a research project, please cite as follows:
```
@inproceedings{tremblay2018corl:dope,
 author = {Jonathan Tremblay and Thang To and Balakumar Sundaralingam and Yu Xiang and Dieter Fox and Stan Birchfield},
 title = {Deep Object Pose Estimation for Semantic Robotic Grasping of Household Objects},
 booktitle = {Conference on Robot Learning (CoRL)},
 url = "https://arxiv.org/abs/1809.10790",
 year = 2018
}
```
## License

Copyright (C) 2018 NVIDIA Corporation. All rights reserved. Licensed under the [CC BY-NC-SA 4.0 license](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode).
    

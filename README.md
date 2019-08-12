# dope_ros_realsense

## ROS Wrapper for Intel® RealSense™ Devices
### Step 1: Install the latest Intel® RealSense™ SDK 2.0
Install from [Debian Package](https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md#installing-the-packages) - In that case treat yourself as a developer. Make sure you follow the instructions to also install librealsense2-dev and librealsense-dkms packages.
OR
Build from sources by downloading the latest Intel® RealSense™ SDK 2.0 and follow the instructions under [Linux Installation](https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md)

### Step 2: Install the ROS distribution
Install ROS Kinetic, on Ubuntu 16.04

### Step 3: Install Intel® RealSense™ ROS from Sources
Create a catkin workspace
  
    mkdir -p ~/catkin_ws/src
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

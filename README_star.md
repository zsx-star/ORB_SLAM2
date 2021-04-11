#### 结合中国大学MOOC软件科技博物馆gazebo世界环境运行ORB_SLAM2

#### 0 要运行SLAM需要事先安装一些库
##### 0.1 安装cmake:
```
sudo apt-get install cmake
```
##### 0.2 安装Pangolin:
```
sudo apt-get install libglew-dev libpython2.7-devel
git clone https://github.com/stevenlovegrove/Pangolin.github
cd Pangolin
mkdir build
cd build
cmake ..
make –j
sudo make install
```
##### 0.3 安装OpenCV:
* 安装依赖
```
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
* 编译安装
http://opencv.org(官网下载2.4.11版本并解压到本地)
cd ~/opencv
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=Release –D CMAKE_INSTALL_PREFIX=/usr/local ..
make –j8
sudo make install
```
##### 0.4 安装Eigen3
```
sudo apt-get install libeigen3-dev
```
##### 0.5 安装git:
```
sudo apt-get install git
```
##### 0.6 安装DBoW2和g2o
此步骤即为第2步骤:安装ORB_SLAM2
sudo chmod +x build.sh
(此时先不执行)
#### 1 下载中国大学MOOC软件科技博物馆gazebo世界环境
* 将以下仓库内容克隆到自己的工作空间,并catkin_make编译
```
git clone https://github.com/zsx-star/ROS-Academy-for-Beginners
source devel/setup.bash
```
* 启动gazebo世界环境
```
roslaunch robot_sim_demo robot_spawn.launch
```
* 启动控制世界中机器人运动节点
roslaunch robot_sim_demo robot_control.launch 

#### 2 安装ORB_SLAM2
* 将以下仓库内容克隆到自己的电脑上
```
git clone https://github.com/zsx-star/ORB_SLAM2.github
cd ORB_SLAM2
sudo chmod +x build.sh
./build.sh
cd Examples/ROS/ORB_SLAM2
mkdir build
cd build
cmake ..
make
```
* 将中国大学MOOC里面世界仿真环境中kinetic相机参数文件，在ROS-Academy-for-Beginners/orbslam2_demo/param/Zdzn.yaml,将其放在/Examples/RGB-D/Zdzn.yaml
* 此仿真环境下，发布的相机图像的话题为/camera/depth/image_raw和/camera/rgb/image_raw，所以我们slam接受话题的数据时名称要一致。打开/src/ORB_SLAM2_ros/Examples/ROS/ORB_SLAM2/src/ros_rgbd.cc进行修改;将其对应的话题名字改为:/camera/depth/image_raw和/camera/rgb/image_raw;

* 运行ORB_SLAM2(路径要改为自己的路径)
```
 rosrun ORB_SLAM2 RGBD /home/zsx/ORB_SLAM2/Vocabulary/ORBvoc.txt /home/zsx/ORB_SLAM2/Examples/RGB-D/Zdzn.yaml
```
* 查看机器人收到的图像
```
rosrun image_view image_view image:=/camera/depth/image_raw
rosrun image_view image_view image:=/camera/rgb/image_raw
```

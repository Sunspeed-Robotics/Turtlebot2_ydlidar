Kobuki/Turtlebot2安装与配置操作说明：
系统版本：Ubuntu 16.04

1.ROS安装：
ROS版本：kinetic 1.12.14
官网：http://wiki.ros.org/kinetic/Installation/Ubuntu

2.底盘与Kinect1配置：
https://blog.csdn.net/yinxingtianxia/article/details/80267536
https://blog.csdn.net/qq_32005213/article/details/80227179

3.ydlidar G4驱动安装：
按照官方文档操作即可（U盘拷贝）

4.kinect1实现建图：
配置环境
echo "export TURTLEBOT_3D_SENSOR=kinect" >> ~/.bashrc
https://blog.csdn.net/qq_35379989/article/details/79017125

配置网络
小车
echo export ROS_MASTER_URI=http://localhost:11311 >> ~/.bashrc
echo export ROS_HOSTNAME=IP_OF_TURTLEBOT >> ~/.bashrc
工作站
echo export ROS_MASTER_URI=http://IP_OF_TURTLEBOT:11311 >> ~/.bashrc
echo export ROS_HOSTNAME=IP_OF_PC >> ~/.bashrc

安装SSH
sudo apt install openssh-server

建图导航
小车主机运行
roslaunch turtlebot_bringup minimal.launch
roslaunch turtlebot_navigation gmapping_demo.launch
工作站运行
roslaunch turtlebot_rviz_launchers view_navigation.launch
(或者 rosrun rviz rviz -d `rospack find turtlebot_rviz_launchers`/rviz/navigation.rviz)
roslaunch turtlebot_teleop keyboard_teleop.launch

保存地图
rosrun map_server map_saver -f $HOME/map/xxx $HOME/map/为地图目录路径，
xxx为地图名称，生成后得到xxx.yaml和xxx.pgm两个文件
加载地图
rosrun map_server map_server $HOME/map/xxx.yaml
roslaunch turtlebot_navigation amcl_demo.launch map_file:=$HOME/xxx.yaml

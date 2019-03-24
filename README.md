# RoboLidar
Using Hector SLAM without odometry data on a ROS system with the RPLidar A1.

1. Clone this repository
2. Clean all build files(`lidar_ws/build, lidar_ws/devel, lidar_ws/src/CMakeLists.txt`). Then run `catkin_make`
3. Run `source /devel/setup.bash`
4. Run `chmod 666 /dev/ttyUSB0` or the serial path to your lidar
5. Run `roslaunch rplidar_ros rplidar.launch`
6. Run `roslaunch hector_slam_launch tutorial.launch`
7. RVIZ should open up with SLAM data
8. If you want to save the map, run `rostopic pub syscommand std_msgs/String "savegeotiff"`.
9. By default, geotiff maps are saved to the 'hector_slam/hector_geotiff/maps' folder. You should find both a .tif file containing the image data and a .tfw file containing the georeference information there. The creation time is appended to the map base name for both files. 

# Sources
[RPLidar Hector SLAM](https://github.com/NickL77/RPLidar_Hector_SLAM)<br />
[RPLidar](https://github.com/robopeak/rplidar_ros)<br />
[Hector_SLAM](https://github.com/tu-darmstadt-ros-pkg/hector_slam)<br />
[Fixing launch files](https://hackaday.io/project/7284-oscar-omni-service-cooperative-assistant-robot/log/26164-first-foray-into-ros) (only needed if you are using the original hector slam repository)
- In `catkin_ws/src/rplidar_hector_slam/hector_slam/hector_mapping/launch/mapping_default.launch` <br />
__replace the second last line with__ <br />
`<node pkg="tf" type="static_transform_publisher" name="base_to_laser_broadcaster" args="0 0 0 0 0 0 base_link laser 100" />`<br />
__the third line with__<br />
`<arg name="base_frame" default="base_link"/>`<br />
__the fourth line with__<br />
`<arg name="odom_frame" default="base_link"/>`
- In `catkin_ws/src/rplidar_hector_slam/hector_slam/hector_slam_launch/launch/tutorial.launch` <br />
__replace the third line with__<br />
`<param name="/use_sim_time" value="false"/>`

Install and Compliation for RTAB-Map:
The detailed information can be found in https://github.com/introlab/rtabmap_ros#installation

1、Instal the ros packages:

sudo apt-get install ros-kinetic-rtabmap-ros/

2、Set environment variables:

Export LD_LIBRARY_PATH=$LD_LIBRARY_PATH: /opt/ros/kinetic/lib/ x86_64-linux-gnu

3、Set the path:

source /opt/ros/kinetic/setup.bash

source ~/catkin_ws/devel/setup.bash

4、Set the dependencies:

sudo apt-get install ros-kinetic-rtabmap ros-kinetic-rtabmap-ros

5、Install RTAB-Map:
git clone https://github.com/introlab/rtabmap.git rtabmap

cd rtabmap/build

Cmake -DCMAKE_INSTALL_PREFIX=~/catkin_ws/devel ..

make

sudo make install

6、Install RTAB in the workspace：

cd ~/catkin_ws

git clone https://github.com/introlab/rtabmap_ros.git src/rtabmap_ros

catkin_make -j1



Usage for RTAB-Map:
1、Run the Kinect V2 command:

roslaunch kinect2_bridge kinect2_bridge.launch publish_tf:=true

2、Execute official instruction tf:

rosrun tf static_transform_publisher 0 0 0 -1.5707963267948966 0 -1.5707963267948966 camera_link kinect2_link 100

///rosrun tf static_transform_publisher 0 0 0 -1.5707963267948966 0 -1.5707963267948966 camera_link kinect2_rgb_optical_frame  100  
 
3、Launch rtabmap_ros：
roslaunch rtabmap_ros rtabmap.launch rtabmap_args:="--delete_db_on_start" rgb_topic:=/kinect2/qhd/image_color_rect depth_topic:=/kinect2/qhd/image_depth_rect camera_info_topic:=/kinect2/qhd/camera_info

///roslaunch rtabmap_ros rgbd_mapping_kinect2.launch resolution:=qhd

4、Map data is saved in ~/.ros/rtabmap.db

The rtabmap db file can be checked as:

rtabmap-databaseViewer ~/.ros/rtabmap.db

5、The three-dimensional point-cloud map can be saved as:

//rosrun pcl_ros pointcloud_to_pcd input:=/kinect2/sd/points

rosrun pcl_ros pointcloud_to_pcd input:=/rtabmap/cloud_map
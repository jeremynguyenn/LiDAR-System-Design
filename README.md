## Contents

1. [Introduction](#introduction)
2. [Mechanical Design and Manufacturing](#mechanical-design-and-manufacturing)
3. [System Architecture](#system-architecture)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Visualization](#visualization)
7. [Results](#results)

# Introduction
To enhance the coverage of a limited-angle 3D LiDAR sensor, a servo motor-driven electromechanical rotation system was developed. This system enables the MRS 1000 3D LiDAR from SICK to capture high-resolution point clouds by rotating along the y-axis, thereby accessing previously unreachable areas. A dedicated ROS package was implemented to manage LiDAR data transformation, mapping, modeling, visualization, servo motor control via rosserial, and IMU integration. The external IMU provides real-time orientation feedback, supporting accurate environment reconstruction. A real-time digital twin of the system was visualized in RViz.

| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/physical_system_montaged.jpg) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/gif2.gif) |
|------------------------------------|------------------------------------|
| 3D LiDAR Rotation System              | Visualization on Rviz               |

---

## Mechanical Design and Manufacturing
The electromechanical system  was designed using Autodesk Fusion 360 and features a robust frame constructed from aluminum profiles. The design incorporates several components manufactured with a 3D printer, ensuring the system’s mechanical integrity and adaptability.
| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/CAD1.png) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/CAD2%20(1).png) | ![Visualization](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/physical_system.gif) |
|:-----------------------------------:|:-------------------------------------:|:-------------------------------------:|
| CAD File                  | CAD File                       | Physical system and Rviz                |


## System Architecture
In this ROS-based system, the integration of a 3D LiDAR rotation mechanism with a SICK MRS 1000 sensor, an IMU, and a servo motor is implemented. The /mcu_imu_gps_servo node orchestrates servo motor positioning and IMU data collection. Raw LiDAR point clouds are published by the /sick_mrs_1xxx node on /cloud. Servo position decoding is managed via /nt16_to_servo_pos and transmitted through /servo_pos_header. Real-time coordinate frame alignment is achieved using /imu_tf_broadcaster and /LIDAR_tf_broadcaster, both publishing to /tf. The /pointCloud_transformer node transforms the raw point cloud data into a global frame, outputting it as /transformed_cloud. Visualization and monitoring are performed in real time using RViz, facilitating system validation and environmental modeling.

| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/rosgraph.png) | 
|------------------------------------|
| RQT GRAPH                          |

| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/frame_tree.png) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/frames.png) |
|------------------------------------|------------------------------------|
| TF Tree              | Frames on Rviz               |

## Installation
```bash
# Create a ROS workspace
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src

# Clone the repository
git clone https://github.com/jeremynguyenn/LiDAR-System-Design.git

# Navigate to the workspace and build the project
cd ~/catkin_ws
catkin_make

# Source the workspace
source devel/setup.bash
```

## Usage
This setup represents a complete pipeline for the 3D LiDAR rotation system. By running these launch files together, the system integrates servo control, IMU data fusion, LiDAR scanning, and visualization, creating a functional and real-time 3D mapping platform.
   
1. imu_gps_servo.launch handles servo control, IMU and GPS data via rosserial.
```bash
roslaunch lidar_rotation imu_gps_servo.launch
```
2. tf_imu_lidar.launch manages the frame transformations.
```bash
roslaunch lidar_rotation tf_imu_lidar.launch
```
3. visualization.launch provides custom Rviz setup for monitoring the system in real-time using markers and PointCloud.
```bash
roslaunch lidar_rotation visualization.launch
```
4. sick_mrs_1xxx.launch handles raw LiDAR data collection and streaming.
```bash
roslaunch sick_scan sick_mrs_1xxx.launch
```
For more details or to download the official SICK drivers, visit the [sic_scan](https://github.com/SICKAG/sick_scan) and [sic_scan_xd](https://github.com/SICKAG/sick_scan_xd) repositories.

Bag File

This project includes a ROS bag file containing recorded data from the LiDAR rotation system. The bag file provides synchronized 3D point cloud data and servo motor position information, which can be used to analyze and visualize the LiDAR's performance in capturing the environment. By replaying this bag file in a ROS environment, users can simulate the system's functionality and test algorithms for 3D mapping, environment perception, and data processing without requiring the physical setup. This allows for a better understanding of the LiDAR's rotational capabilities and its application in real-world scenarios.

Use rosbag terminal tool to replaying the bag file
```bash
rosbag play tf_transformation_visualization.bag 
```
Using visualization launch file you can visualize movements and sensor readings
```bash
roslaunch lidar_rotation visualization.launch
```

| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/terminal_setup.png) | 
|------------------------------------|
| Terminal Setup                     |

## Visualization
| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/gif0.gif) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/gif1.gif) |
|------------------------------------|------------------------------------|
| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/gif3.gif) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/gif4.gif) |
## Results
| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/face.png) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/indoor.png) |
|------------------------------------|------------------------------------|
| ![LiDAR System](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/segmantation.png) | ![LiDAR in Action](https://github.com/jeremynguyenn/LiDAR-System-Design/blob/main/3D-LiDAR-Rotation-System-Design/images/human.png) |

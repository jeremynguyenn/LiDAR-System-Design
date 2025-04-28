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

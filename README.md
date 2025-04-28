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

| ![LiDAR System](https://github.com/omerdurmus61/3D-LiDAR-Rotation-System-Design/blob/master/images/physical_system_montaged.jpg) | ![LiDAR in Action](https://github.com/omerdurmus61/3D-LiDAR-Rotation-System-Design/blob/master/images/gif2.gif) |
|------------------------------------|------------------------------------|
| 3D LiDAR Rotation System              | Visualization on Rviz               |

---

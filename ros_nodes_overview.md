# ROS Nodes Overview

The software stack is built on the Robot Operating System (ROS). Below is an overview of the primary node structure and data flow connecting the sensors to the control algorithms.

## 1. Sensor Driver Nodes
These nodes interface directly with hardware over serial/USB and publish ROS-compatible messages.
- **`/lidar_node`**: Reads raw serial data from the LiDAR and publishes `sensor_msgs/LaserScan`, capturing distance measurements across a 2D plane.
- **`/camera_node`**: Captures frames and publishes compressed `sensor_msgs/Image`.
- **`/imu_node`**: Reads high-frequency I2C/Serial IMU data, publishing `sensor_msgs/Imu` to report orientation and acceleration.
- **`/sonar_array_node`**: Publishes structured arrays of `sensor_msgs/Range` from the ultrasonic sensors.
- **`/base_controller_node`**: Publishes `nav_msgs/Odometry` based on precise wheel encoder ticks, tracking the physical rotation of the wheels to estimate distance traveled.

## 2. Localization and SLAM Nodes
- **SLAM Architecture**: Subscribes to laser scans and the odometry transform. It aligns incoming LiDAR scans to build a coherent map and publishes a `nav_msgs/OccupancyGrid`. 
- **Sensor Fusion Entity**: Fuses IMU and wheel odometry to provide a robust `odom -> base_link` transform, dampening encoder drift using inertial data.

## 3. Navigation Stack
- **`/move_base`**: The core action server for navigation. 
  - *Global Planner*: Calculates the macro-level path from the robot's current pose to the user-supplied goal.
  - *Local Planner*: Generates immediate command velocities, computing trajectories that avoid sudden obstacles while progressing along the global path.
  
## Data Flow Summary

The end-to-end data pipeline is structured as follows:

```
Sensors -> Driver Nodes -> [Topics: /scan, /odom, /imu] -> SLAM & EKF -> Map + Pose -> Planners -> [Topic: /cmd_vel] -> Base Controller -> Motor Drivers -> Wheels
```

# Autonomous Mobile Robot (AMR)

> **Disclaimer**: This repository contains partial implementation details and architectural overviews to demonstrate system design capability. As this is an ongoing project, full source code and proprietary algorithms are not openly exposed.

## Project Overview

The Autonomous Mobile Robot (AMR) is a ROS-based indoor navigation platform. It utilizes SLAM (Simultaneous Localization and Mapping) to perceive its environment, avoid obstacles, and navigate autonomously. The system integrates multiple sensor streams (LiDAR, Camera, IMU, Ultrasonic, and Wheel Encoders) to achieve robust real-time localization and path planning.

## Problem Statement

Indoor environments offer unique navigation challenges including dynamic obstacles, uniform corridors lacking distinct features, and constrained operational spaces. The objective of this project is to develop a reliable mobile robotic platform capable of safe, autonomous indoor navigation without reliance on external positioning systems (e.g., GPS).

## System Architecture

The software architecture is heavily decoupled, relying on the ROS publisher/subscriber paradigm for asynchronous communication between sensor drivers, the SLAM engine, the navigation stack, and the low-level motor controllers.

```text
[ Hardware & Sensors ]           [ ROS Environment ]                    [ Motor Control ]
                                                                        
 LiDAR ---------------\       /--> Lidar Node ---\                      
 Camera ---------------\     /---> Vision Node ---\                     
 IMU ------------------|    /----> IMU Node ------|                      
 Ultrasonic -----------+---|-----> Sonar Node ----+---> SLAM & NAV --> Base Controller --> Motors
 Wheel Encoders -------/    \----> Encoder Node --/     (Mapping,      (Velocity cmds)
                                                        Pathfinding,
                                                        Obstacle 
                                                        Avoidance)
```
*Sensors → ROS Nodes → SLAM → Navigation → Control*

## Hardware Stack

- **LiDAR**: Primary sensor for 2D mapping and obstacle detection.
- **Camera**: Provides visual context and potential integration for visual odometry.
- **IMU**: Supplies high-frequency orientation and acceleration data for short-term dead reckoning.
- **Ultrasonic Sensors**: Act as a short-range safety net for detecting transparent or highly reflective obstacles.
- **Wheel Encoders**: Provide intrinsic odometry feedback to track wheel rotation and estimate displacement.

## Software Stack

- **Core Framework**: Robot Operating System (ROS)
- **Localization & Mapping**: SLAM engine for real-time occupancy grid generation.
- **Navigation**: ROS Navigation Stack featuring local and global planners.
- **Control**: Differential drive kinematics translated into PID-regulated motor control signals.

## Key Features

- **Autonomous Navigation**: Capable of point-to-point indoor navigation using a generated map.
- **Obstacle Avoidance**: Real-time detection and dynamic path re-planning.
- **Sensor Fusion**: Integration of multiple modalities (LiDAR, IMU, Odometry) for enhanced pose estimation.
- **Modular ROS Architecture**: Decoupled node design allowing straightforward upgrades to individual components.

## My Role

As Team Lead and Robotics Systems Engineer, my responsibilities include:
- Leading the overall system design and establishing the software/hardware architecture.
- Developing and tuning the ROS software stack, including sensor integration and SLAM/navigation parameters.
- Coordinating the hardware integration loop, ensuring robust sensor mounting, precise electronics integration, and safety.

## Demo

*(Placeholder for high-quality video demonstration of the robot navigating a test environment)*

`[Insert Demo Video or GIF here]`

## Future Work

- **Outdoor & Campus Scaling**: Extending the navigation capabilities to handle mixed indoor/outdoor environments over larger areas.
- **Advanced Path Planning**: Implementing more sophisticated algorithms for dynamic, high-traffic scenarios.
- **Fleet Management**: Adjusting the architecture to support multiple decentralized robots operating in the same workspace.

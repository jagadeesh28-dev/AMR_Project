# System Architecture

This document expands on the core system architecture governing the AMR. 

## Architectural Principles

1. **Modularity**: The system relies heavily on the ROS publisher/subscriber model. Each physical sensor has a corresponding independent ROS node.
2. **Redundancy**: State estimation is not dependent on a single sensor. The fusion of LiDAR, IMU, and Encoders creates a resilient odometry pipeline.
3. **Safety First**: Low-level safety overrides are implemented both in firmware and via the high-level ROS navigation stack.

## High-Level Data Flow

1. **Perception**: Sensors publish raw data to specific ROS topics.
2. **Filtering**: Node clusters filter and fuse this data (e.g., using an Extended Kalman Filter) to form a coherent base link state.
3. **Planning**: 
    - The Global Planner computes the optimal route from A to B on the static map.
    - The Local Planner generates velocity commands (`cmd_vel`) to follow the global path while avoiding dynamic obstacles.
4. **Actuation**: The base controller converts `cmd_vel` (linear/angular velocity) into individual wheel speeds, sending commands to the microcontrollers driving the motors.

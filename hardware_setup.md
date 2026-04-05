# Hardware Setup

The Autonomous Mobile Robot (AMR) relies on robust hardware integration to ensure sensor reliability, accurate state estimation, and stable real-world operation.

## Component Overview

1. **Compute Unit**: Provides the high-level processing power for the ROS master, SLAM, and Path Planning algorithms.
2. **Microcontroller**: Handles hard-real-time tasks and PWM generation.
3. **Sensors**:
   - **LiDAR**: Mounted centrally at the highest point of the robot to provide an unobstructed 2D view of the environment.
   - **Camera**: Forward-facing, mounted to provide a wide field of view for visual context and debugging.
   - **IMU**: Mounted rigidly and precisely as close to the robot's center of mass as possible to minimize translational acceleration artifacts during rotation.
   - **Ultrasonic Sensors**: Positioned around the chassis perimeter to act as a fail-safe, covering LiDAR blind spots (e.g., highly reflective glass or low-lying objects).
   - **Wheel Encoders**: Intimately integrated with the drive train to provide high-resolution feedback on motor rotation.
4. **Motor Drivers**: Capable of supplying sufficient sustained current for the chosen drive motors without thermal throttling.
5. **Power Distribution**: Utilizing regulated step-down and step-up converters to isolate and provide stable voltage rails to sensitive sensors and compute units, separate from the electrically noisy motor circuits.

## Integration Approach

- **Wiring and Signal Integrity**: Segregated logic and power wiring routing is employed to reduce electromagnetic interference (EMI). Appropriate shielding and twisted pairs are used for high-frequency, low-voltage signals such as encoder ticks and I2C buses.
- **Physical Mounting**: Custom rigidly designed brackets map each sensor to the robot's fundamental coordinate frame, ensuring physical transforms mirror the static transforms defined in the software stack.

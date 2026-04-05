# System Design

## Overview

The AMR system is designed to operate asynchronously. The compute payload is handled by an onboard processing unit, while real-time motor control and sensor polling are delegated to embedded microcontrollers.

## Design Constraints

- **Compute limitations**: The chosen onboard computer has thermal and processing limits; computationally heavy nodes (like high-res vision processing) must be profiled and throttled dynamically.
- **Power Budget**: The system operates on an internal battery, requiring efficient node operation and power management.

## Control Loop

- **High-level Loop (ROS)**: Operates at ~10-20 Hz. Responsible for localization, mapping, and macro-planning.
- **Low-level Loop (Microcontroller)**: Operates at >100 Hz. Responsible for PID motor control and reading high-frequency encoder ticks.

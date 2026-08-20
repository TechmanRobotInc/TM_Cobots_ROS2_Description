# TM_Cobots_ROS2_Description

This repository contains the official ROS 2 Robot description files (URDF/Xacro) and 3D meshes for Techman Robot's **TM AI Cobot S** and **TM AI Cobot** series. These files are essential for robot visualization (**RViz**), simulation (**Gazebo**), and motion planning (**MoveIt 2**).

---

## 1. Supported Robot Models

The repository provides comprehensive coverage for the following model configurations:

*   **TM AI Cobot S Series:** 
    *   **Standard:** TM5S, TM6S, TM7S, TM12S, TM14S, TM20S
    *   **Standard-X:** TM5SX, TM6SX, TM7SX, TM12SX, TM14SX, TM20SX
    *   **FT module:** TM5SFT, TM6SFT, TM7SFT, TM12SFT, TM14SFT, TM20SFT, TM25SFT, TM30SFT
    *   **FT-X module:** TM5SXFT, TM6SXFT, TM7SXFT, TM12SXFT, TM14SXFT, TM20SXFT, TM25SXFT, TM30SXFT
*   **TM AI Cobot Series:** 
    *   **Standard:** TM5-900, TM5-700
    *   **Standard-X:** TM5X-900, TM5X-700

---

## 2. Support Package Matrix

Each robot model includes verified data mapped across four primary configurations:
1.  **Standard:** Base robot model with the integrated eye-in-hand camera.
2.  **Standard-X:** Model variants without the integrated camera module.
3.  **FT module:** Model featuring an integrated Force-Torque sensor at the flange.
4.  **FT-X module:** Model featuring a Force-Torque sensor but excluding the integrated camera.

| Hardware Configuration Matrix | Eye-in-Hand Camera | Flange Force-Torque (FT) Sensor |
| :---: | :---: | :---: |
| **Standard** | ✅ Integrated | ❌ None |
| **Standard-X** | ❌ None | ❌ None |
| **FT Module** | ✅ Integrated | ✅ Integrated |
| **FT-X Module** | ❌ None | ✅ Integrated |


---

## 3. Directory Structure Examples

The repository adheres to standard ROS 2 package conventions. Below are directory tree examples showing how configurations are mapped for different series.

### Example A: TM AI Cobot S Series (e.g., TM12S)
Located under the `cobot_s/` subdirectory:
```bash
tm_description/cobot_s/tm12s_description/
                       ├── launch/            # ROS 2 launch scripts
                       ├── meshes/            # 3D visualization & collision models
                           ├── tm12s/         # Standard meshes
                           ├── tm12sx/        # X-variant meshes
                           ├── tm12sft/       # Force-Torque variant meshes
                           └── tm12sxft/      # X + Force-Torque variant meshes
                       ├── rviz/              # RViz2 configuration files
                       ├── xacro/             # Parameterized robot description source files
                       ├── CMakeLists.txt     # Build configuration
                       └── package.xml        # ROS 2 package dependencies metadata
```

### Example B: TM AI Cobot Series (e.g., TM5-900)
Located under the `cobot/` subdirectory:
```bash
tm_description/cobot/tm5_900_description/
                       ├── launch/            # ROS 2 launch scripts
                       ├── meshes/            # 3D visualization & collision models
                           ├── tm5-900/       # Standard meshes
                           └── tm5x-900/      # X-variant meshes
                       ├── rviz/              # RViz2 configuration files
                       ├── xacro/             # Parameterized robot description source files
                       ├── CMakeLists.txt     # Build configuration
                       └── package.xml        # ROS 2 package dependencies metadata
```

---

## 4. Quick Start

Verify that the robot description files and 3D meshes load correctly into the coordinate frame workspace by launching the state publisher.

### Instruction Syntax

```bash
ros2 launch <tm_robot_series>_description view_robot.launch.py robot_model:=<tm_robot_type>
```

#### Parameter Requirements
* **`<tm_robot_series>`**: The lowercase designation of the TM Robot series (e.g., `tm12s`, `tm6s`, `tm30s`).
* **`<tm_robot_type>`**: The exact lowercase model identifier of the TM Robot (e.g., `tm12s`, `tm12sx`, `tm12sft`, or `tm12sxft`).

---

### Example: Visualizing the TM12SFT Robot

Follow these step-by-step commands to source your workspace and launch the visualization interface:

```bash
# 1. Source the workspace environment
source ~/tm2_ws/install/setup.bash

# 2. Launch the robot visualization
ros2 launch tm12s_description view_robot.launch.py robot_model:=tm12sft
```

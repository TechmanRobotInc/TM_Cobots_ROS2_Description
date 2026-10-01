# TM_Cobots_ROS2_Description

This repository contains the official ROS 2 Robot description files (URDF/Xacro) and 3D meshes for the Techman Robot's **TM AI Cobot S** and **TM AI Cobot** series. These files are essential for robot visualization (**RViz2**), simulation (**Gazebo**), and motion planning (**MoveIt 2**).

---

## 1. Support Package Matrix

The repository provides comprehensive coverage for the **TM AI Cobot S** and **TM AI Cobot** series. Each robot model includes verified data mapped across four primary hardware configurations:

[1]&nbsp; **Standard Configuration:** &nbsp; Base robot model equipped with the integrated **Eye-in-Hand Camera** module.<br>
[2]&nbsp; **Standard-X Configuration:** &nbsp; Pure robotic arm variant designed **without** the camera module at the flange.<br>
[3]&nbsp; **FT Configuration:** &nbsp; Advanced variant featuring both the **Eye-in-Hand Camera** and an integrated **Force-Torque (FT) Sensor**.<br>
[4]&nbsp; **FT-X Configuration:** &nbsp; Specialized variant equipped with the **Force-Torque (FT) Sensor** but **excluding** the camera module.<br>

### TM AI Cobot S and TM AI Cobot Series Model Matrix
<table>
  <thead>
    <tr>
      <th rowspan="2"></th>
      <th rowspan="2">Series</th>
      <th colspan="4" style="text-align: center;">Xacro model name</th>
    </tr>
    <tr>
      <th style="text-align: center;">Standard</th>
      <th style="text-align: center;">Standard-X</th>
      <th style="text-align: center;">FT</th>
      <th style="text-align: center;">FT-X</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>TM AI Cobot S Series</b></td>
      <td><b>TM5S</b></td>
      <td align="center">tm5s</td>
      <td align="center">tm5sx</td>
      <td align="center">tm5sft</td>
      <td align="center">tm5sxft</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM6S</b></td>
      <td align="center">tm6s</td>
      <td align="center">tm6sx</td>
      <td align="center">tm6sft</td>
      <td align="center">tm6sxft</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM7S</b></td>
      <td align="center">tm7s</td>
      <td align="center">tm7sx</td>
      <td align="center">tm7sft</td>
      <td align="center">tm7sxft</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM12S</b></td>
      <td align="center">tm12s</td>
      <td align="center">tm12sx</td>
      <td align="center">tm12sft</td>
      <td align="center">tm12sxft</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM14S</b></td>
      <td align="center">tm14s</td>
      <td align="center">tm14sx</td>
      <td align="center">tm14sft</td>
      <td align="center">tm14sxft</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM20S</b></td>
      <td align="center">tm20s</td>
      <td align="center">tm20sx</td>
      <td align="center">tm20sft</td>
      <td align="center">tm20sxft</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM25S</b></td>
      <td align="center">—</td>
      <td align="center">—</td>
      <td align="center">📌 <b>tm25sft</b></td>
      <td align="center">📌 <b>tm25sxft</b></td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM30S</b></td>
      <td align="center">—</td>
      <td align="center">—</td>
      <td align="center">📌 <b>tm30sft</b></td>
      <td align="center">📌 <b>tm30sxft</b></td>
    </tr>
    <tr>
      <td><b>TM AI Cobot Series</b></td>
      <td><b>TM5-700</b></td>
      <td align="center">tm5-700</td>
      <td align="center">tm5x-700</td>
      <td align="center">—</td>
      <td align="center">—</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM5-900</b></td>
      <td align="center">tm5-900</td>
      <td align="center">tm5x-900</td>
      <td align="center">—</td>
      <td align="center">—</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM12</b></td>
      <td align="center">tm12</td>
      <td align="center">tm12x</td>
      <td align="center">—</td>
      <td align="center">—</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM14</b></td>
      <td align="center">tm14</td>
      <td align="center">tm14x</td>
      <td align="center">—</td>
      <td align="center">—</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM16</b></td>
      <td align="center">tm16</td>
      <td align="center">tm16x</td>
      <td align="center">—</td>
      <td align="center">—</td>
    </tr>
    <tr>
      <td></td>
      <td><b>TM20</b></td>
      <td align="center">tm20</td>
      <td align="center">tm20x</td>
      <td align="center">—</td>
      <td align="center">—</td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> **Xacro Model Name to New Official TM Robot Name Mapping:**<br>
> &emsp;📌 `tm25sft` → Corresponding Official Model: **TM25S**<br>
> &emsp;📌 `tm25sxft` → Corresponding Official Model: **TM25SX**<br>
> &emsp;📌 `tm30sft` → Corresponding Official Model: **TM30S**<br>
> &emsp;📌 `tm30sxft` → Corresponding Official Model: **TM30SX**<br>

---

## 2. Directory Structure Examples

The repository adheres to standard ROS 2 package conventions. Below are directory tree examples showing how configurations are mapped for different series.

### Example A: TM AI Cobot S Series (e.g., TM12S)
Located under the TM12S series configuration subdirectory:

```bash
tm2_ws/ or ros2_ws/ or user_ws/            # User's workspace root directory
└── tm2_ros2/                              # TM ROS 2 standard source code directory (Acts as the 'src' space)
    └── tm_description/                    # Robot Model Description Module
        └── cobot_s/                       # TM Cobot S-Series folder
            └── tm12s_description/         # TM12S 3D meshes, URDF models, and Xacro files
                ├── launch/                # ROS 2 launch scripts
                ├── meshes/                # 3D visualization & collision models
                │   ├── tm12s/             # Standard meshes
                │   ├── tm12sx/            # X-variant meshes
                │   ├── tm12sft/           # Force-Torque variant meshes
                │   └── tm12sxft/          # X + Force-Torque variant meshes
                ├── rviz/                  # RViz2 configuration files
                ├── xacro/                 # Parameterized robot description source files
                ├── CMakeLists.txt         # Build configuration
                └── package.xml            # ROS 2 package dependencies metadata
```

### Example B: TM AI Cobot Series (e.g., TM5-900)
Located under the TM5-900 series configuration subdirectory:

```bash
tm2_ws/ or ros2_ws/ or user_ws/            # User's workspace root directory
└── tm2_ros2/                              # TM ROS 2 standard source code directory (Acts as the 'src' space)
    └── tm_description/                    # Robot Model Description Module
        └── cobot/                         # TM AI Cobot series folder
            └── tm5_900_description/       # TM5-900 3D meshes, URDF models, and Xacro files
                ├── launch/                # ROS 2 launch scripts
                ├── meshes/                # 3D visualization & collision models
                │   ├── tm5-900/           # Standard meshes
                │   └── tm5x-900/          # X-variant meshes
                ├── rviz/                  # RViz2 configuration files
                ├── xacro/                 # Parameterized robot description source files
                ├── CMakeLists.txt         # Build configuration
                └── package.xml            # ROS 2 package dependencies metadata
```

---

## 3. Quick Start

Verify that the robot description files and 3D meshes load correctly into the coordinate frame workspace by launching the state publisher.

### Instruction Syntax

```bash
ros2 launch <tm_robot_series>_description view_robot.launch.py robot_model:=<tm_robot_type>
```

#### Parameter Requirements
* **`<tm_robot_series>`**: The lowercase designation of the TM Robot series (e.g., `tm12s`, `tm6s`, `tm5-900`).
* **`<tm_robot_type>`**: The exact lowercase model identifier of the TM Robot (e.g., `tm12sft`, `tm6sx`, `tm5x-900`).

---

### Example: Visualizing the TM12SFT Robot

Follow these step-by-step commands to source your workspace environment and launch the RViz2 visualization interface:

```bash
# 1. Source the workspace environment
source ~/tm2_ws/install/setup.bash

# 2. Launch the robot visualization
ros2 launch tm12s_description view_robot.launch.py robot_model:=tm12sft
```

# TM_Cobots_ROS2_Description
:bookmark_tabs: TM ROS2 version **<ins>Jazzy or higher</ins>** is strictly required to support the TM Robots Series directory structure syntax.

This repository provides essential ROS 2 description files (URDF/Xacro) and 3D meshes for the **TM AI Cobot S** and **TM AI Cobot** series. It supports various configurations, including Standard, Standard-X, FT module, and FT-X for robot visualization (**RViz**), simulation (**Gazebo**), and motion planning (**MoveIt 2**).
- [Usage Guideline](./tm_description/TM_Cobots_ROS2_Description.md)

Additionally, this guide (below) details **how to migrate these standalone description packages into a legacy `tm2_ros2` workspace**.

---

## 1. Quick Reference Table

The repository provides comprehensive coverage for the following model configurations:
|  | Standard | Standard-X | FT Module | FT-X Module |
| :---  | :---: | :---: | :---: | :---: |
| **TM AI Cobot S Series** | TM5S  | TM5SX | TM5SFT | TM5SXFT |
|  | TM12S  | TM12SX | TM12SFT | TM12SXFT |
| **TM AI Cobot Series** | TM5-700 | TM5X-700 | — | — |
|  | TM5-900 | TM5X-900 | — | — |

> 💡 **Note:** Robot models are continuously updated and deployed to this repository.

---

## 2. Migration & Deployment Guide

### Integrating Standalone Descriptions into Legacy `tm2_ros2` Workspace

This guide explains how to migrate robot description files for the **TM AI Cobot S Series** (e.g., `tm5s`) into the legacy `tm2_ros2` workspace. The legacy repository only includes the `tm12s` profile by default. Missing profiles must be retrieved from the standalone [TM_Cobots_ROS2_Description](https://github.com/TechmanRobotInc/TM_Cobots_ROS2_Description) repository.

### Directory Structure Reference
Your workspace **must** maintain the exact layout below to prevent dependency failures and path resolution issues:

```text
user_ws/ or tm2_ws/
└── tm2_ros2/
    └── tm_description/
        └── cobot_s/
            ├── tm12s_description/    <-- Default robot description profile in the tm2_ros2 Jazzy (legacy) repo
            └── tm5s_description/     <-- Newly migrated standalone package from TM_Cobots_ROS2_Description repo
                ├── launch/
                ├── meshes/
                ├── rviz/
                ├── xacro/
                ├── CMakeLists.txt
                └── package.xml
```

---

### Method A: Manual Selective Deployment

Use Git sparse-checkout to download and pull only the specific model files you need.

#### 1. Clone and Filter the Repository
```bash
# Initialize a partial clone without downloading file blobs
git clone --filter=blob:none --no-checkout https://github.com/TechmanRobotInc/TM_Cobots_ROS2_Description
cd TM_Cobots_ROS2_Description

# Configure the sparse-checkout engine for the target model
git sparse-checkout init --cone
git sparse-checkout set tm_description/cobot_s/tm5s_description

# Pull only the matching files from the main branch
git checkout main
```

#### 2. Copy the Package to Your Workspace
Ensure the destination directory structure exists, then run the appropriate command for your environment: (For example: ~/tm2_ws/tm2_ros2/tm_description/cobot_s/)

*   **Case 1: Standard Linux Environment**
    ```bash
    cp -r tm_description/cobot_s/tm5s_description ~/tm2_ws/tm2_ros2/tm_description/cobot_s/
    ```
*   **Case 2: Target workspace is located under a mounted D Drive Linux Environment (WSL2 / Linux)**
    ```bash
    cp -r /mnt/d/TM_Cobots_ROS2_Description/tm_description/cobot_s/tm5s_description /mnt/d/tm2_ws/tm2_ros2/tm_description/cobot_s/
    ```

💡 **Tip:** Replace `tm5s_description` with `tm7s_description` or other target models as required.

---

### Method B: Automated Deployment (via Script)

Automate the retrieval and deployment process using the workspace loader script.

#### Step 1: Update `user_workspace.txt`
Edit your configuration file to define the root path of your active ROS 2 workspace:

```bash
# ---- Custom Setup (Specify the root directory of your ROS 2 workspace) ----
# Ensure this points to your active tm2_ros2 workspace (e.g., your Jazzy workspace)
WS_ROOT=$HOME/user_ws/tm2_ros2
```
> 📄 Path Workspace Configuration [`user_workspace.txt`](https://github.com/TechmanRobotInc/tm2_ros2/tree/jazzy/configs/tm_loader/user_workspace.txt)

#### Step 2: Execute the Loader Script
Run the script (⚡ lite_ld.sh) to download and map the package automatically:

```bash
# Grant executable permissions to the deployment script if needed:
chmod +x lite_ld.sh

# Fetch and deploy the target model description package:
./lite_ld.sh tm5s

# Use the force flag (-f) to overwrite existing legacy files if updating:
# ./lite_ld.sh tm12s tm_description -f
```
> 🗂️ The Loader Script [`tm_loader` tool](https://github.com/TechmanRobotInc/tm2_ros2/tree/jazzy/configs/tm_loader/)

---

## 3. Post-Deployment Verification & Compilation

⚠️ **Important:** If you have previously compiled the workspace or added new application packages, you **must** purge old build artifacts. Failing to clean the workspace may cause ROS 2 indexing mismatches and compilation errors.

Run the following sequence in your terminal to perform a clean rebuild:

```bash
# 1. Source the system ROS 2 environment and set DDS middleware
source /opt/ros/jazzy/setup.bash
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp

# 2. Navigate to your workspace root directory
cd ~/tm2_ws

# 3. Purge legacy build, install, and log directories
rm -rf build install log

# 4. Perform a clean workspace build with optimization flags
colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release

# 5. Source the newly built workspace environment
source ./install/setup.bash
```

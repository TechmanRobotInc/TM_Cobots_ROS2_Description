# Migration & Deployment Guide

### Integrating Standalone Descriptions into Legacy `tm2_ros2` Workspace
This guide explains how to migrate robot description files for the **TM AI Cobot S Series** (e.g., `tm5s`) into the legacy `tm2_ros2` workspace.

> The legacy repository only includes the `tm12s` profile by default. Missing profiles must be retrieved from the standalone [TM_Cobots_ROS2_Description](https://github.com/TechmanRobotInc/TM_Cobots_ROS2_Description) repository.

> [!NOTE]
> <sub>*   **TM ROS2 Jazzy Apps ⬆️**: TM ROS2 version **Jazzy or higher** is strictly required to support the TM Robots Series directory structure syntax.</sub><br/>
> <sub>*   **Git Engine**: Git version **2.25 or higher** is strictly required to support native sparse-checkout engine syntax.</sub><br/>

### 📂 Directory Structure Reference
Your workspace **must** maintain the exact layout below to prevent dependency failures and path resolution issues:

> 🔍 Migrated Package Layout Overview 
> 
> ```diff
> user_ws/ or tm2_ws/
> └── tm2_ros2/
>     └── tm_description/
>         └── cobot_s/
>             ├── tm12s_description/    <-- Default robot description profile in the tm2_ros2 Jazzy (legacy) repo
> +           └── tm5s_description/     <-- Newly migrated standalone package from TM_Cobots_ROS2_Description repo
>                 ├── launch/
>                 ├── meshes/
>                 ├── rviz/
>                 ├── xacro/
>                 ├── CMakeLists.txt
>                 └── package.xml
> ```

---

### 🛠️ Integrating Standalone Descriptions into a Legacy `tm2_ros2` Workspace

> ### 🚀 Method A: Automated Deployment (via Script) `[Recommended]`
> 
> 📖 The Loader Script [Usage Guideline](https://github.com/TechmanRobotInc/tm2_ros2/tree/jazzy/configs/tm_loader/README.md) and [tools](https://github.com/TechmanRobotInc/tm2_ros2/tree/jazzy/configs/tm_loader/)
>
> Automate the retrieval and deployment process using the workspace loader script.
> 
>> ```bash
>> ./lite_ld.sh [MODEL] [PACKAGE (optional)] [-f (optional)]
>> ```
>> 
>> #### 📝 Argument Options
>> *   **`[MODEL]` (Required)**: `tm5s`, `tm12s`, `tm14s`, etc.
>> *   **`[PACKAGE]` (Optional)**: `tm_description`, `tm_moveit`, `tm_gazebo`.
>>
>> #### 📍 Step 1: Update `user_workspace.txt`
>> Edit your configuration file to define the root path of your active ROS 2 workspace:
>> 
>> ```bash
>> # ---- Custom Setup (Specify the root directory of your ROS 2 workspace) ----
>> # Ensure this points to your active tm2_ros2 directory (e.g., assume your active ROS workspace name is tm2_ws)
>> WS_ROOT=$HOME/tm2_ws
>> ```
>> 📄 Path Workspace Configuration [`user_workspace.txt`](https://github.com/TechmanRobotInc/tm2_ros2/tree/jazzy/configs/tm_loader/user_workspace.txt)
>> 
>> #### 📍 Step 2: Execute the Loader Script
>> Run the script (⚡ lite_ld.sh) to download and map the package automatically:
>> 
>> ```bash
>> # Grant executable permissions to the deployment script if needed:
>> chmod +x lite_ld.sh
>> 
>> # Fetch and deploy the target model description package(e.g., `tm5s`):
>> ./lite_ld.sh tm5s
>> 
>> # Use the force flag (-f) to overwrite existing legacy files(e.g., `tm12s`) if updating:
>> #./lite_ld.sh tm12s tm_description -f
>>```
>>

---

> ### 🚀 Method B: Manual Selective Deployment
> 
> Use Git sparse-checkout to download and pull only the specific model files you need.
> 
>> #### 📍 Step 1: Clone and Filter the Repository
>> ```bash
>> # Initialize a partial clone without downloading file blobs
>> git clone --filter=blob:none --no-checkout https://github.com/TechmanRobotInc/TM_Cobots_ROS2_Description
>> cd TM_Cobots_ROS2_Description
>> 
>> # Configure the sparse-checkout engine for the target model(e.g., `tm5s`) 
>> git sparse-checkout init --cone
>> git sparse-checkout set tm_description/cobot_s/tm5s_description
>> 
>> # Pull only the matching files from the main branch
>> git checkout main
>> ```
>> 
>> #### 📍 Step 2: Copy the Package to Your Workspace
>> Ensure the destination directory structure exists, then run the appropriate command for your environment: *(For example: `~/tm2_ws/tm2_ros2/tm_description/cobot_s/`)*
>> 
>> *   **Case 1: Standard Linux Environment**
>>     ```bash
>>     cp -r tm_description/cobot_s/tm5s_description ~/tm2_ws/tm2_ros2/tm_description/cobot_s/
>>     ```
>> *   **Case 2: Target workspace is located under D Drive Linux Environment (WSL2 / Linux)**
>>     ```bash
>>     cp -r /mnt/d/TM_Cobots_ROS2_Description/tm_description/cobot_s/tm5s_description /mnt/d/tm2_ws/tm2_ros2/tm_description/cobot_s/
>>     ```
>> 
>> 💡 **Tip:** Replace `tm5s_description` with `tm7s_description` or other target models as required.
>>

---

## &sect; Post-Deployment Verification & Compilation

⚠️ **Important:** If you have previously compiled the workspace or added new application packages, you **must** purge old build artifacts. Failing to clean the workspace may cause ROS 2 indexing mismatches and compilation errors.

> Run the following sequence in your terminal to perform a clean rebuild:
> 
> ```bash
> # 1. Source the system ROS 2 environment and set the DDS middleware
> source /opt/ros/jazzy/setup.bash
> 
> export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
> 
> # 2. Navigate to your workspace root directory
> cd ~/tm2_ws
> 
> # 3. Purge legacy build, install, and log directories
> rm -rf build install log
> 
> # 4. Perform a clean workspace build with optimization flags
> colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
> 
> # 5. Source the newly built workspace environment
> source ./install/setup.bash
> ```

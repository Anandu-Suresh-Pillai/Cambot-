```markdown
# CamBot

CamBot is a 7-DoF robot with a depth camera and a multi-camera system attached to its tool flange.  
This repository contains the files required to simulate CamBot in a ROS 2 environment and visualize it in Gazebo and RViz2.

[Optional badges: build, license, ros2]

Overview
--------
CamBot's package(s) include URDF/xacro descriptions, Gazebo launch files, and RViz configurations to:
- Simulate the robot in Gazebo
- Visualize the robot and sensor data in RViz2
- Provide example launch files for easy startup

Requirements
------------
- ROS 2 (tested on Humble and newer)
- Gazebo with the `gazebo_ros` packages installed
- colcon for building (colcon-common-extensions recommended)
- Typical dev tools (git, python3, etc.)

Installation
------------
Create a workspace, clone the repo and build:

```bash
# create workspace
mkdir -p ~/cambot_ws/src
cd ~/cambot_ws/src

# clone the repository
git clone https://github.com/Anandu-Suresh-Pillai/Cambot-.git

# return to workspace root
cd ~/cambot_ws

# source your ROS 2 install (replace <distro> if needed)
source /opt/ros/<distro>/setup.bash

# install dependencies (if package has package.xml / rosdep entries)
# sudo apt update
# sudo apt install -y python3-rosdep
# sudo rosdep init   # run only once per machine
# rosdep update
# rosdep install --from-paths src --ignore-src -r -y

# build
colcon build --symlink-install

# source the overlay
source install/setup.bash
```

Notes:
- Replace `<distro>` with your ROS 2 distribution (e.g., `humble`, `iron`).
- If you run into missing dependencies, use rosdep as shown above.

Running the simulation (Gazebo)
------------------------------
To launch the robot in Gazebo:

```bash
# From workspace where install/setup.bash is sourced
ros2 launch cambot_description gazebo.launch.py
```

This should open Gazebo with the CamBot model spawned. If the world or sensors do not appear, check the console for missing plugins or topic errors.

Running the visualization (RViz2)
---------------------------------
To view the robot in RViz2:

```bash
ros2 launch cambot_description display.launch.py
```

This will open RViz2 using the provided RViz configuration (if present). Use the "Fixed Frame" consistent with your TF (commonly `base_link` or `world`).

Images / Screenshots
--------------------
Replace the placeholder links below with repository-stored images under `docs/` or `media/` and reference them with raw GitHub URLs (raw.githubusercontent...) for reliable rendering.

Example placeholder images:
![Gazebo preview](docs/images/gazebo_preview.png)
![RViz preview](docs/images/rviz_preview.png)

Repository layout (expected)
---------------------------
- cambot_description/    — URDF / xacro, meshes, Gazebo & RViz launch files
- cambot_control/        — controllers and config (optional)
- launch/                — convenience launch files
- docs/ or media/        — screenshots and documentation

Troubleshooting
---------------
- Gazebo plugin errors: verify `gazebo_ros` and plugin dependencies are installed for your ROS 2 distro.
- No TF / missing frames in RViz: ensure the robot_state_publisher node is running and you have sourced the correct setup.bash.
- Build issues: try `colcon build --symlink-install --event-handlers console_cohesion+` to get clearer output.

Contributing
------------
Contributions are welcome. Please:
1. Open an issue describing the change or bug.
2. Create a branch from `main`.
3. Submit a pull request with a clear description and link to any related issue.


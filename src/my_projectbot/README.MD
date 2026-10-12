# My ProjectBot
An Autonomous differential-drive robot simulation built with **ROS 2 (Humble)**, **Gazebo**, and the **NAV2** stack.
---

## Demonstration
* [Watch the Autonomous Navigation Demo](https://drive.google.com/file/d/1OsyBcyIwFwhZ2_yAz0ZsEzaLHL8GPKlc/view?usp=drivesdk)

---

## Features
- **Robot Modeling**: Custom URDF/XACRO differential-drive robot equipped with LiDAR and depth camera plugins.
- **Mapping & Localization**: SLAM-generated 2D map with AMCL (Adaptive Monte Carlo Localization).
- **Autonomous Navigation**: Nav2 path planning with dynamic obstacle avoidance.
- **Velocity Routing**: 'twist_mux' configuration to prioritize manual teleoperation over autonomous planner commands.

---

## Running the Simulation
To Run this project, open four separate terminals and execute the following commands.
*(NOTE: Make sure you have built the workspace using 'colcon build' before running).*

### Terminal 1: Launch the Robot in Gazebo
```bash
source /opt/ros/humble/setup.bash
source ~/project_ws/install/setup.bash
ros2 launch my_projectbot launch_sim.launch.py

```

### Terminal 2: Launch Localization
*(NOTE: **map:=** argument points to the saved map. Make sure have that setup or you can to manually built you own)*
```bash
source /opt/ros/humble/setup.bash
source ~/project_ws/install/setup.bash
ros2 launch my_projectbot localization_launch.py map:=/home/navneet555/project_ws/src/my_projectbot/maps/my_map.yaml use_sim_time:=true

```

### Terminal 3: Launch Navigation
```bash
source /opt/ros/humble/setup.bash
source ~/project_ws/install/setup.bash
ros2 launch my_projectbot navigation_launch.py use_sim_time:=true

```

### Terminal 4: Launch Rviz Visualization
```bash
source /opt/ros/humble/setup.bash
ros2 run rviz2 rviz2 -d /opt/ros/humble/share/nav2_bringup/rviz/nav2_default_view.rviz --ros-args -p use_sim_time:=true

```


### Usage Instructions
- Once all terminals are running, Rviz and Gazebo will Open.
- In RViz, use the **2D Pose Estimate** tool to set the robot's initial position on the map.
- Use the **2D Goal Pose** tool to set a destination.
- The NAV2 stack will calculate the path and the Robot will autonomously navigate to the goal in Gazebo.
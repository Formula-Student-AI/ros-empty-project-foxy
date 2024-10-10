# README

This repository contains the .devcontainer files for VSCode to build a Ubuntu 20.04 docker container with ROS 2 Foxy installed as part of the articu-project team project.

## Versions
- OS: Ubuntu 20.04 (Focal)
- ROS: ROS 2 Foxy

## Instructions

0. See https://github.com/Formula-Student-AI/ros-docker for instructions for how to setup .devcontainers in VSCode.

1. Navigate to your home folder and clone this repo
   ```
   git clone https://github.com/Formula-Student-AI/articu-project
   ```

2. Reopen in Container
   - Open the cloned repository in VSCode.
   - Click on the blue box in the bottom left-hand corner of the VSCode window.
   - Select "Reopen in Container".

3. Make src directory to store ROS packages and `cd` into it
   ```
   mkdir src
   cd src
   ```

4. Clone the ball_tracker ROS package
   ```
   git clone https://github.com/joshnewans/articubot_one
   ```

5. Clone the ball_tracker ROS package
   ```
   git clone https://github.com/joshnewans/ball_tracker
   ```

6. `cd` back into workspace and build the packages
   ```
   cd ..
   colcon build --symlink-install
   ```

7. Source the overlay
   ```
   source install/setup.bash
   ```

8. Launch the world
   ```
   ros2 launch articubot_one launch_sim.launch.py world:=./src/articubot_one/worlds/obstacles.world
   ```

9. Put tennis ball in gazebo models paths
   ```
   sudo cp -r tennis_ball/ /usr/share/gazebo-11/models/
   ```

10. Open a new terminal, source the overlay again, and launch the ball tracker
   ```
   source install/setup.bash
   ros2 launch ball_tracker ball_tracker.launch.py params_file:=./src/articubot_one/config/ball_tracker_params_sim.yaml 
   ```

10. Now you can spawn in a tennis ball into the Gazebo sim and the robot will follow it! (To spawn in the tennis ball, you will need to add /articu-project to the path by going to Insert -> Add Path -> Computer -> '/' -> Choose 'articu-project'. Then you can insert the tennis ball as a model and move it around.).


## Credit
- [ijnek](https://github.com/ijnek/ros-devcontainer-template)
- [Josh Ewans](https://github.com/joshnewans)

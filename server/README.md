# About
![image](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/30937261/83c70ad3-a01d-4923-b111-fafad9d02742)

The server has two main functions:
- Computing the screw axis parameters from AR-HMD data points (Step 4 above), and
- Transfering a plan from the AR-HMD to the robot (Step 9b above)

# Package Overview
The server functions are implemented using the [ar_screw_axis package](https://github.com/UTNuclearRobotics/ar_screw_axis.git).

# Installation
Install the server software **on a host connected to the Robofleet network**. The server software is designed for Ubuntu 20.04/ROS Noetic.
```
cd ~
mkdir -p my_server_ws/src
cd ~/my_server_ws/src
git clone https://github.com/UTNuclearRobotics/ar_screw_axis.git
cd ~/my_server_ws
catkin build
source devel/setup.bash
```

# Usage
On a host connected to the Robofleet network, in a properly-sourced ROS workspace, launch the demo script:
```
roslaunch ar_screw_axis screw_axis_demo.launch
```
This will launch:
- The server's robofleet client
- The `nlls_solver` screw axis solver node
- The transform listener
- A `similarity_study` node to compute simililarity metrics and save the data

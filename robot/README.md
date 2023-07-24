# About
This ```ar-affordances/robot``` directory has all the information and linked packages required to perform manipulations that were defined by the user wearing an AR-HMD.

# Prerequisites
## Hardware
- Mobile Manipulator with SLAM Capabilities
- RGB-D Sensor (minimum)
- Local Wireless Network
  
## Software
The following packages must be installed and configured on robot hardware to localize and communicate with AR-HMD users. Follow the links below to install and configure each component.

### Integrate Robot into AugRE Ecosystem
1. Follow [UTNuclearRobotics/afc_demos](https://github.com/UTNuclearRobotics/afc_demos) installation and configuration instructions.[^1]
[^1]: [UTNuclearRobotics/afc_demos](https://github.com/UTNuclearRobotics/afc_demos) will provide details on how to install a [RobofleetClient](https://github.com/UTNuclearRobotics/robofleet_client) on the robot as well as all the necessary [Microsoft Azure Spatial Anchor](https://learn.microsoft.com/en-us/azure/spatial-anchors/overview) code necessary to communicate and localize with AR-HMD users.

### Temoto Framework
1. Follow [temoto-framework](https://github.com/temoto-framework/temoto/wiki) installation and configuration instructions.

# Run Demo
The ar-affordance demo uses the vbats affordance primitive package that runs on board the robot and solves ... (blah, blah, blah). Error correction packages are used by pausing the affordance primitive packages in this spot ... (blah, blah, blah). Follow along with the following instructions to install and run the demo.

## Dependencies
```
sudo apt install python3-vcstools
```
## Environment Setup
1. Create a catkin workspace and clone this repo into the ```catkin_ws/src``` directory.
```
git clone https://github.com/UTNuclearRoboticsPublic/ar-affordances.git
```
2. Clone packages required to run this demo via vcstools.
```
cd ar-affordances/robot && vcs import < .robot.repos
```

### Affordance Primitive Package Setup
1. Change into the vbats repo and do stuff
```
cd robot/vbats && #do stuff
```

### Error Correction Method Setup
- #### Eye-To-Hand Calibration (EHC)
  1. TODO: detail hololens visuals
     
- #### Feel-in-the-Dark Exploration (FitD)
  1. Change into the robot_static repo and do stuff
  ```
  cd robot/robot_statics && #do stuff
  ```
  
- #### k-Nearest Neighbor Regression (k-NN)
  1. Change into the knn repo and do stuff
  ```
  cd robot/knn && #do stuff
  ```
  
- #### Point Cloud Segmentation (PC Seg)
  1. Change into the pc_seg repo and do stuff
  ```
  cd robot/pc_seg && #do stuff
  ```

## Running Demo
* Start TeMoto
``` bash 
roslaunch vaultbot_temoto_config temoto.launch temoto_namespace:=vaultbot
```
* Load the robot
``` bash 
roslaunch ta_initialize_robot invoke_action.launch wake_word:=vaultbot
```
* Start camera components
``` bash 
roslaunch ta_start_component invoke_action.launch wake_word:=vaultbot
```
* Main launch file that contains core components to connect to AugRE. [robofleet_client, robot_augre, anchor_spatial_azure]
``` bash 
cd afc_catkin_ws
source devel/setup.bash
roslaunch afc_demos full_demo.launch robot:=vaultbot use_database:=true agent_type:=ugv_manip camera_name:=camera_left camera_image_name:=color
```

Once the robot is initialized and localized, we can command it to perfomr a task. 

The user, using the HMD (Hololens 2) performs a demostration on an object to define the screw axis and the grasp point, which internally generates a UMRF graph that contains a sequence of TeMoto actions in a JSON format (string), that is sent to the robot through robofleet using the ```/broadcast_start_umrf_graph``` topic. 

When TeMoto receives the UMRF graph, it validates if all of the TeMoto actions exist and starts the graph from the root node or first TeMoto action.


## Requirements:

<details>
<summary>Required TeMoto Actions:</summary>

|TeMoto Action|Description|Input Parameters|
|---|---|---|
| ta_initialize_robot       | Brings up the robot and its main capabilities: Navigation, maniulation, and gripper features| robot_name |
| ta_start_component        | TeMoto action used to load the cameras| component | 
|ta_move_manip_target_pose  |Moves the manipulator to a named target pose pre defined on the srdf |robot_Name planning_group target_pose|
|ta_move_base               |Action that sends a navigation goal for the mobile base. Use to approach to the object.             |robot_name reference_frame pose_2d(x,y,theta)|
| ta_move_gripper           | Controls the openning of the gripper | robot_name position(0_100%) |
| ta_screw_vector           | Validates the trajectory from multiple screws, and moves the arm to the start pose | robot_name planning_group end_effector_name screw_array grab_pose |
| ta_state_ap               | TeMoto action used to perform the screws (approach, turn valve, and retreat motion) | robot_name ap_action_name end_effector_name screw_frame is_pure_tranlation screw_axis screw_origin screw_distance screw_pitch task_impedance_rotation tansk_impedance_translation thate_dot|
| ta_find_grasp             | Performs the exploration methods to find a valid grasp pose | robot_name gripper_name clase_tolerance |



</details>
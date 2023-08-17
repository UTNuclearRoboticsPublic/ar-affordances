# About
This ```ar-affordances/robot``` directory has all the information and linked packages required to perform manipulations that were defined by the user wearing an AR-HMD.

# Prerequisites
## Hardware
- Mobile Manipulator with SLAM Capabilities
- RGB-D Sensor (minimum)
- Local Wireless Network
  
## Software
The following packages must be installed and configured on both the robot hardware and on an operator workstation machine. If using Vaultbot (Demo Robot) these packages are already installed and configured. If setting up a new robot, the list of software packages below is the minimum requirements for peforming this demo. You will still need basic packages on board to run sensors, manipulators, navigation, etc. Follow the links below to learn more about each package, duplicate, and leverage if needed.
|Package Name|Description|
|---|---|
| [affordance_primitives](https://github.com/UTNuclearRobotics/affordance_primitives.git) | This is the high-level repository for Affordance Primitives (APs). |
| [ap_planning](https://github.com/UTNuclearRobotics/ap_planning.git) |  Code for pre-planning kinematic trajectories for screw-based Affordance Primitives. | 
| [compliance_controller](https://github.com/UTNuclearRobotics/compliance_controller.git) | Code to enable or disable compliance required for manipulation. |
| [affordance templates (vbats)](https://github.com/UTNuclearRobotics/vbats.git) | This repo is a VaultBot-specific AT code, partnered with the robot-agnostic affordance_primitives repository. New robots will need a similar repo setup. |
| [temoto-framework](https://github.com/temoto-framework/temoto/wiki) | TeMoto actions must be created for navigation, manipulation, etc. See drop-down list below. | 

<details>
<summary>Required TeMoto Actions:</summary>

|TeMoto Action|Description|Input Parameters|
|---|---|---|
| ta_initialize_robot       | Brings up the robot and its main capabilities: Navigation, maniulation, and gripper features| robot_name |
| ta_start_component        | TeMoto action used to load the cameras| component | 
|ta_move_manip_target_pose  |Moves the manipulator to a named target pose pre defined on the srdf | robot_name <br> planning_group <br> target_pose|
|ta_move_base               |Action that sends a navigation goal for the mobile base. Use to approach to the object.             |robot_name <br> reference_frame <br> pose_2d(x,y,theta)|
| ta_move_gripper           | Controls the openning of the gripper | robot_name <br> position(0_100%) |
| ta_screw_vector           | Validates the trajectory from multiple screws, and moves the arm to the start pose | robot_name <br> planning_group <br> end_effector_name <br> screw_array <br> grab_pose |
| ta_state_ap               | TeMoto action used to perform the screws (approach, turn valve, and retreat motion) | robot_name <br> ap_action_name <br> end_effector_name <br> screw_frame <br> is_pure_tranlation <br> screw_axis <br> screw_origin <br> screw_distance <br> screw_pitch <br> task_impedance_rotation <br> tansk_impedance_translation <br> thate_dot|
| ta_find_grasp             | Performs the exploration methods to find a valid grasp pose | robot_name <br> gripper_name <br> clase_tolerance |

</details>

### Using Vaultbot (Dual Arm Robot Used in Demo)
- *Onboard*: The packages listed in the above table should all be installed onboard Vaultbot. If there are issues, the [vaultbot_onboard (Github)](https://github.com/UTNuclearRobotics/vaultbot_onboard) repo is the main repo used to install everything again. Follow instructions on the ReadMe to install the necessary software onboard.
  | :exclamation:  make sure you used ```git submodule update --init --recursive``` to get all submodules |
  |-----------------------------------------|
  
  | :exclamation: Use ```noetic``` branch (as of 8/17/2023) |
  |-----------------------------------------|
- *Operator:* If the operator machine is not already configured for controlling vaultbot. [vaultbot_control](https://github.com/UTNuclearRobotics/vaultbot_control) is a combination of everything you need to get the packages up and running on your local machine.

### AugRE Integration 
- Instructions below will get your robot integrated into the AugRE framework used for AR-based human-robot interactions. The following packages are required to communicate and localize with AR (Microsoft HoloLens 2) users. If using Vaultbot, this is already all installed.
1. Follow [UTNuclearRobotics/afc_demos](https://github.com/UTNuclearRobotics/afc_demos) installation and configuration instructions.[^1]
[^1]: [UTNuclearRobotics/afc_demos](https://github.com/UTNuclearRobotics/afc_demos) will provide details on how to install a [RobofleetClient](https://github.com/UTNuclearRobotics/robofleet_client) on the robot as well as all the necessary [Microsoft Azure Spatial Anchor](https://learn.microsoft.com/en-us/azure/spatial-anchors/overview) code necessary to communicate and localize with AR-HMD users.

### Error Correction Method Setup
- #### Eye-To-Hand Calibration (EHC)
  1. TODO: detail hololens visuals
     
- #### Feel-in-the-Dark Exploration (FitD)
  1. Change into the robot_static repo and do stuff
  ```
  cd robot/robot_statics && #do stuff
  ```
  
- #### k-Nearest Neighbor Regression (k-NN)
  1. At a properly sourced workspace on the robot, launch the k-NN grasp refinement server:
  ```
  rosrun vbats nn_pose_correction_server
  ```
  Ensure the `/mega/calibration_mode` parameter is set to `'john'`.
  
  Now, invoke the `ta_screw_vector` action, and the k-NN grasp correction service will be used.
  
- #### Point Cloud Segmentation (PC Seg)
  1. Change into the pc_seg repo and do stuff
  ```
  cd robot/pc_seg && #do stuff
  ```

# Running Demo

Follow the instructions linked on the [VB TeMoto Operator](https://github.com/UTNuclearRobotics/vb_temoto_operator.git) repo. Direct link to demo: [Hololens Integration Demo](https://github.com/UTNuclearRobotics/vb_temoto_operator/tree/turn_valve_demo#hololens-integration-demo)

 -NOTE: These instructions below are specific to Vaultbot, but if using a new robot, the steps will still be the same, just different naming conventions may be used.

## Continue Setup
Once the robot is initialized and localized, we can command it to perform a task. Follow the [Server README](https://github.com/UTNuclearRoboticsPublic/ar-affordances/blob/main/server/README.md) next to setup the required server for solving screw axis parameters and then follow instructions on [ARHMD README](https://github.com/UTNuclearRoboticsPublic/ar-affordances/blob/main/arhmd/README.md) to deploy and launch AugRE application with the ADAM module.

### Details
The user, using the HMD (Hololens 2) performs a demonstration on an object to define the screw axis and the grasp point, which internally generates a UMRF graph that contains a sequence of TeMoto actions in a JSON format (string), that is sent to the robot through robofleet using the ```/broadcast_start_umrf_graph``` topic. 

When TeMoto receives the UMRF graph, it validates if all of the TeMoto actions exist and starts the graph from the root node or the first TeMoto action.

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
1. Follow [temoto-framework/temoto](https://github.com/temoto-framework/temoto) installation and configuration instructions.

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
1. Run the basic roslaunch file & ...
```
roslaunch super_mega_demo
```

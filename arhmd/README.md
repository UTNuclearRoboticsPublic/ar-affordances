# About
This ```ar-affordances/arhmd``` directory has all information and package links required to install and run the Microsoft HoloLens 2 AR-HMD application used to capture 
user demonstrations and command the robot to perform manipulations on the object in focus. The AR-HMD is responsible for tracking the user's hands and visualizing the various items to the user that are shown below.

# Dependencies
Install vcstools to get started using this directory
```
sudo apt install python3-vcstools
```

# Installation
1. Create a catkin workspace and clone this repo into the ```catkin_ws/src``` directory [^1].
[^1]: If you are not going to use any of the ```ar-affordances/robot``` or ```ar-affordances/server``` code on your current machine, and just want to obtain the HoloLens 2 executable application, then you can work out of any directory.
```
git clone https://github.com/UTNuclearRoboticsPublic/ar-affordances.git
```
2. Clone required AR-HMD packages via vcstools.
```
cd ar-affordances/arhmd && vcs import < .arhmd.repos
```
3. Download the Microsoft HoloLens 2 executable. 
```
bash .get-hololens-pkg
```
4. [Open the Windows Device Portal](https://learn.microsoft.com/en-us/windows/mixed-reality/develop/advanced-concepts/using-the-windows-device-portal#connecting-over-wi-fi) and [install](https://learn.microsoft.com/en-us/windows/mixed-reality/develop/advanced-concepts/using-the-windows-device-portal#installing-an-app)
the ```AugRE.appxbundle``` and ```AugRE.cer``` to your HoloLens 2 that are now in the ```ar-affordances/arhmd/HololensPkg_AugRE_v2.9.0-alpha``` directory.

# Application Instructions
#### TODO

# Contributing
- You can download and modify the release of the AugRE project used for this paper by cloning the ```v2.9.0-alpha``` AugRE release.
  ```
  cd ar-affordances/arhmd && bash .get-release-code
  ```
- See [UTNuclearRobotics/Augmented-Robot-Environment](https://github.com/UTNuclearRobotics/Augmented-Robot-Environment) to get started contributing to the lastest AugRE developments.


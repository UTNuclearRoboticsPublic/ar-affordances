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
the ```AugRE.appxbundle``` and ```Microsoft.VCLibs.arm64.14.00.appx``` to your HoloLens 2 that are now in the ```ar-affordances/arhmd/HololensPkg_AugRE_v2.9.0-alpha``` directory.

# Application Instructions
1. Turn on HoloLens 2 and sign in (passwords are on stache for all HoloLens')
2. Open the "AugRE" application and start the "ADAM" module.
    <details>
    <summary>a. From the HoloLens home menu, tap on "All Apps"</summary>
    
    ![tap_on_all_apps_image.](https://user-images.githubusercontent.com/84527482/223891696-45f13847-2dd3-4bde-9494-6db12c321cbe.jpg)
    
    </details>
    <details>
    <summary>b. Select "AugRE". You may need to use the scroll button on the right side to scroll down in the list.</summary>
    
    ![tap_on_scroll_down_image.](https://user-images.githubusercontent.com/84527482/223892013-99a2215c-9c1a-4704-831f-b1632f881584.jpg)

    </details>
    <details>
    <summary>c. Use an open palm facing yourself to open the hand menu.</summary>
    
    ![hand_menu](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/39d2c252-5690-4270-b4e6-a8936945ee37)

    </details>
    <details>
    <summary>c. Use an open palm facing yourself to open the hand menu and tap on the "More" button.</summary>
    
    ![hand_menu](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/39d2c252-5690-4270-b4e6-a8936945ee37)

    </details>
    <details>
    <summary>d. With the utility menu open, tap on the "Define" button.</summary>

    ![utility_menu](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/c271cbce-1321-4e19-af03-1083c787fc8c)

    </details>
3. When the ADAM module opens after tapping the "Define" button, you must first localize to a QR code in the scene. Do this by enabling the camera (if it asks) and look at the QR code. The device is ready to capture your hands once the QR code is lit up green.
    <details>
    <summary>a. Look at the QR code until it is highlighted.</summary>

    ![look_at_qr_code](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/82a8799b-70f9-4785-9feb-d6304f677a97)

    </details>
    <details>
     <summary>b. When highlighted, the QR code will turn green.</summary>

    ![qr_code_highlights](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/a6576f9d-e8ca-414c-a9e9-e21e05a06070)

    </details>
4. (Recommended, but optional) In the scene, there is a virtual gripper. Align this to the gripper attached to the robot to calibrate the gripper.
    <details>
    <summary>a. Find the calibration menu in the scene. (Shown in the image below)</summary>

    ![calibration_menu](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/1b94eea9-374e-4140-a6c9-f4b58bd7817f)

    </details>
    <details>
    <summary>b. Once the gripper is aligned with the robot gripper, tap on "Calibrate". This creates a calibration transform.</summary>

    ![calibration_image](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/03ba64d2-1283-4c78-b884-89bb42500b15)

    </details>
5. At this point, you are ready to send definitions to the robot. You must make sure the NLLS server is running first, though, before you can send it definitions. (See ...)
    <details>
    <summary>a. To define an object manipulation, first, select whether it is a liner or rotational definition on the calibration menu.</summary>

    ![calibration_menu](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/1b94eea9-374e-4140-a6c9-f4b58bd7817f)

    </details>
    <details>
    <summary>b. Once assigned, use the voice command "Start Grip" and "End Grip" to start and stop tracking a trajectory.</summary>

    ![start_stop_grip](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/e5182e25-a5a9-4a1a-943a-17c2643707bf)

    </details>
    <details>
    <summary>c. Wait until the screw axis is visualized in the scene. Once visualized, you can tap on the "Publish" and the robot will receive the Temoto graph to begin execution.</summary>

    ![20230222_082730_HoloLens](https://github.com/UTNuclearRoboticsPublic/ar-affordances/assets/84527482/e9fd7ad5-cd47-40d3-8267-56ece9b98c0c)

    </details>
    
# Contributing
- You can download and modify the release of the AugRE project used for this paper by cloning the ```v2.9.0-alpha``` AugRE release.
  ```
  cd ar-affordances/arhmd && bash .get-release-code
  ```
- See [UTNuclearRobotics/Augmented-Robot-Environment](https://github.com/UTNuclearRobotics/Augmented-Robot-Environment) to get started contributing to the latest AugRE developments.


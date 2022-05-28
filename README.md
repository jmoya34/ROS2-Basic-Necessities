# Setting up ROS2
A timeline on how to learn ROS2. I will be refering to the offcial [ROS2 documentation](https://docs.ros.org/en/foxy/index.html) as well as [Raymond Andrade's ROS2 robotics developer Course.](https://www.udemy.com/course/ros2-robotics-developer-course-using-ros2-in-python/)


## Installation
An advantage of ROS2 over ROS1 is the combaility with Windows, Mac, and Linux. The path I recommend when working with robotics is Linux due to jetson nanos and raspberry pi's using Linux. If you have a Mac or Windows device trying to follow Linux guide, I recommend using a virtual machine. Go into [Virtual Machine setup](VirtualMachineSetup)
* Here is the official documentation for installing [ROS2 Foxy Distro](https://docs.ros.org/en/foxy/Installation.html)

## Framework Overview
ROS offers a Data Distribution service (DDS) which is the communication pipline interfaces with all excuting code. The excuting files using ROS functionality are known as **Nodes**

### Nodes have 3 ways of communication:
* **Publisher** nodes sending infromation that allow for **Subscriber** nodes to recive information.
* **Services** sends a request to a **Service server** that when completes a request will send back a response
* **Actions** will send a goal which the **Actions server** will process the goal and send progress updates to the client that sent the goal. This process is known as **Feedback**.

### Node Parameters:
* Parameters are usefull for taking change into account instead of editing the source code and recompiling the project. 
* Parameters can be edited by **the user** OR **other nodes** to change parameters.

### Bag files:
* Bag files are usefull when you want to collect data.
* You are able to play back the information.
* A usefull example of this would be recording videos.

### Packages:
* Packages contain all code for a robots functionality.
* Packages can be shared between users to replicate with their own rebot.
* You are able to incorporate other packages along with your own as well.

## Creating Workspaces
Your startign directory doesn't matter. I personally like seeing my files on the desktop so I create my workspaces as such on Linux.

```bash
moya@:~/Desktop/ros_workspace$
```

Create workspaces inside the **ros_workspace directory** labeled as anything  you wish, and I will label mine as **learning_ws**. Inside the learning_ws include a new directory called src. Inside the src folder, run the following ros2 command to create a package
```bash
moya@:~/Desktop/ros_workspace/learning_ws/src$ ros2 pkg create learning_ws_pkg --build-type ament_cmake
```
**Note: you should see a folder with the package name and the following folders appear inside the package folder**

![folders](/imgs/amentcmake.png)

### Create Scripts folder:
* In the same directory as the cmakelists.txt file, create a folder for future scripts that we are goign to make.

### Building package using colcon:
* Going back to our workspace directory in terminal, we are going to use colcon to build our package. For reference, the path should look something like this:
```bash
moya@:~/Desktop/ros_workspace$
```

* **[IMPORTANT]** Every time we adding a script or make a change to a script we have to rebuild the package using colcon.
* The following command is used to install colcon on Ubuntu
```bash
sudo apt install python3-colcon-common-extensions
```
* Using colcon is as simple as running the command
```bash
moya@:~/Desktop/ros_workspace$ colcon build
```
* There should be 3 new folders labled
1. build
2. install
3. log
* To include the package to the terminal enviornment use comamnds
```bash
moya@:~/Desktop/ros_workspace$ source install/setup.bash
```

## Configuring Packages
Everytime we add a new node to our package we have to configure out cmakelist.txt and package.xml file so the complier involves the newly created scripts.

1. In package.xml add the new following lines under line 10
```xml
<buildtool_depend>ament_cmake_python</buildtool_depend>
<depend>rclpy</depend>
```
![Visual Representation of how package.xml might look](/imgs/packxml.png)

2. Everytime we add a new node, we must write it down in CMakeLists.txt. Under line 19 in the CMakeLists.txt file write the following lines of code
```
# find dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)
find_package(rclpy REQUIRED)
ament_python_install_package(scripts/)
```
* **[IMPORTANT]** Colcon build will fail if you do not create a __init__.py file inside scripts file!
* Using the command will allow your nodes to be included as such. There is no limit to the amount of nodes you wish to add. In the example below, I have a publisher and subscriber node inside my scripts folder that I am attempting to associate with my package.
```
install(PROGRAMS
scripts/publisher.py
scripts/subscriber.py
DESTINATION lib/${PROJECT_NAME}
)
```
* Please note that if the top of the python script does not inolve a ```#! /usr/bin/env python3``` then colcon report an error. Look at examples for more info.

3. By going back into workspace directory we can colcon and source the package 
```bash
moya@:~/Desktop/ros_workspace$ colcon build
moya@:~/Desktop/ros_workspace$ source install/setup.bash
```
* To check if it properly included the scripts as nodes run the following command
```bash
ros2 pkg executables <your_pkg>
```
<br>

# Developing ROS2 skills in python


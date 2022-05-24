# ROS2-Basic-Necessities
A timeline on how to learn ROS2. I will be refering to the offcial [ROS2 documentation](https://docs.ros.org/en/foxy/index.html) as well as [Raymond Andrade's ROS2 robotics developer Course.](https://www.udemy.com/course/ros2-robotics-developer-course-using-ros2-in-python/)

## Installation
An advantage of ROS2 over ROS1 is the combaility with Windows, Mac, and Linux. The path I recommend when working with robotics is Linux due to jetson nanos and raspberry pi's using Linux. If you have a Mac or Windows device trying to follow Linux guide, I recommend using a virtual machine. Go into [Virtual Machine setup](VirtualMachineSetup)

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

## Developing ROS2 skills in python


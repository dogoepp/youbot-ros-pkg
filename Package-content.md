The information written here about the content of each meta-package (formerly known as stacks) are the result of a quick observation of the source code. We publish it in the hope that it helps understand the structure of this repository but it may be inaccurate or even wrong. If you made any deeper investigation, please update this file or write an issue so that we can update it.

## youbot_applications

This meta-package's only package, hanoi seems to have been used for a Hanoi tower contest at some point. I don't think that it is going to be useful for us.

However, it has some code for inverse kinematics of the YouBot arm. Who knows, it may be of some use one day.

## youbot_common

### youbot_description
Contains description files for the base and arms in URDF and other formats (actually in xacro that has to be converted). Also has launch files for controller programs, test programs and so on.

### youbot_trajectory_action_server
Contains a class for an action server for the YouBot. This class is compiled as a library (static or shared ?).

## youbot_diagnostics

### youbot_battery_monitor
**ROS-independant program that displays on the embedded screen the battery voltage and IP adresses of eth0 and wlan0. If roscore is already running, it also sends the information as topics. There is a README for more details.**

### youbot_dashboard
**A Python software meant to create a GUI for YouBot. It uses wxPython. To be tested !**

### youbot_diagnostic_aggregator
Launches the diagnostic_aggregator node from the ROS diagnostics metapackage (to be downloaded) for the YouBot. This node aggregates and re-publishes diagnostic messages from the youbot analyzers (see config file).

## youbot_manipulation

### simple_trajectory_controller
A trajectory controller for the arm.

## youbot_navigation

### youbot_navigation_common
There are two kinds of contents:

- a node that does a low pass filter on velocity commands (recieves them from the commanding node, does the filtering and sends to youbot base)
- launch files, for the hokuyo lidar and one for complete navigation system (using the hokuyo)

## youbot_navigation_global
Not investigated.

## youbot_navigation_local
Not investigated.

## youbot_oodl
This package contains the controller node that interfaces the native API and driver with ROS. This is started with the launch file `youbot_oodl_driver.launch`.

## youbot_perception
Not investigated
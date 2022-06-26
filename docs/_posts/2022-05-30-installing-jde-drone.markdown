---
layout: posts
title:  "Installing JDE Drones"
date:   2022-05-30 16:29:33 +0530
categories: gsoc
---
Getting started with my GSoC period, one of my goals during the project was to make drone applications using Visual Circuit.
[JdeRobot's Academy](http://jderobot.github.io/RoboticsAcademy/) already has some great exercises related to drones and their basic concepts, my job was to get a solution running using Visual Circuit.

![Drone Exercises](/gsoc2022-Toshan_Luktuke/assets/academy_drones.png)

The challenge here was to get the exercises running locally on my system. This is because drone based exercises are usually very complicated to get running, with a lot of packages and dependencies there are many areas where one can mess up an installation. 
Unfortunately a lot of JdeRobot's support for these exercises is moved online onto their Docker Image, while it is a great way for newcomers to get the exercises running with little or no difficulty, it wasn't going to work for me.

In the following blog I'm going to be describing how I got these exercises running locally, the errors I encountered and how I solved each one:

### My Laptop Configuration

<table>
<tr>
<td>OS</td>
<td>Ubuntu 20.04 LTS</td>
</tr>
<tr>
<td>ROS</td>
<td>Noetic</td>
</tr>
</table>

![Neofetch Output](/gsoc2022-Toshan_Luktuke/assets/neofetch_output.png)

### The Process
To start with I followed [this](https://github.com/JdeRobot/drones/blob/noetic-devel/installation20.md) guide on the JdeRobot drones repo. 

The 'drones' repo contains the main dependencies needed to run the exercises

You also need to install these packages 
```bash
sudo apt-get install ros-noetic-jderobot-drones
```

While building the files in my `catkin_ws` I was encountering an error with the import of the `teleopWidget`.

Apparently Python couldn't detect the path, despite being in the same directory.

I changed the import to a relative import:

`from teleopWidget import TeleopWidget` ----> `from .teleopWidget import TeleopWidget` 

As soon as I solved this error, I encountered another one however. This time with a package name `qfi`. Apparently it wasn't being found.

I found this [GitHub issue](https://github.com/JdeRobot/RoboticsAcademy/issues/847) and this [StackOverflow thread](https://stackoverflow.com/questions/71928676/cannot-find-module-qfi-for-running-jderobot-drone-cat-mouse-exercise-from-sour?newreg=016111d2131f47fcbddec5ed5ed05ffa) about it.

The solution was to clone this repository called [ThirdParty](https://github.com/JdeRobot/ThirdParty) by JdeRobot. Within `qflightinstruments/python` we can find the `qfi` module. Now we have to add this to our where our Python distribution stores its packages.

```bash
cd ~
git clone https://github.com/JdeRobot/ThirdParty
cd ~/ThirdParty/qflightinstruments/python
cp -r qfi /usr/lib/python3/dist-packages/ # This is for my case
# cp -r qfi /usr/lib/python2.7/dist-packages/ Might work for some people
```
Finally I tried running the `follow_road` exercise.

The issue this time was that Gazebo took far too long to launch. Upon launching I found that the drone model hadn't spawned it.

It looked like my Gazebo model path did not include the JdeRobot `drone_assets` from the `drones` repo.

```bash
echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/catkin_ws/src/drones/drone_assets/models" >> ~/.bashrc
```
The above lines will append the `drone_assets` repo to your Gazebo model path whenever you start a terminal session.

After this, I got `follow_road` launched, and could get the drone moving via the RQT controller.

Next, I had to launch `drone_cat_and_mouse`, here there was another error saying a package called `xmlstartlet` wasn't found. I referred to this [issue](https://discuss.px4.io/t/cannot-load-command-parameter-vehicle-spawn-sdf-launch/16284) and simply installed it via the terminal. 
```bash
sudo apt install xmlstarlet
```
 The exercise launched fine after this. 

 However there is a warning that frequently pops up on the terminal for most of these exercises. In order to silence that warning, simply do this

 ```bash
 roslaunch follow_road.launch 2> >(grep -v TF_REPEATED_DATA ignore)
 ``` 

Image of warning:
![Repeated Data Warning](/gsoc2022-Toshan_Luktuke/assets/repeated_data_warning.png)
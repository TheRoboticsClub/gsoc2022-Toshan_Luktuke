---
layout: posts
title:  "Week 5: Coding Period"
date:   2022-07-24 23:15:00 +0530
categories: gsoc
---
 This was a week where I started to work on the Finite State Machine that I had mentioned in my proposal.

 ## FSM

 The start was simple enough, first I had to find a world to run the robot in. My mentors suggessted the Vacuum Cleaner exercise from Robotics Academy or Bump and Go. I initially tried setting up Bump and Go's world on my computer.

 However it used a `kobuki` robot or rather a `kobuki_node` dependency of the bot. Despite checking multiple sources on the internet I wasn't able to find a way to install it through the ros package manager. This left me one option i.e. to build from source, over here I followed a few tutorials but quickly realised that the errors I was getting would be quite troublesome to solve, and it would be easier to simply try the Vacuum Cleaner world once.

 For the Vacuum Cleaner bot I had to download the [Custom Robots](https://github.com/JdeRobot/CustomRobots) repo from JdeRobot. I placed this repo in my `catkin_ws` and added the models to my `$GAZEBO_MODEL_PATH` soon after it launched perfectly.

 My approach to the FSM was as follows:

 ![Insert Image here soon](/gsoc2022-Toshan_Luktuke/assets/fsm-diagram.png)

 With 3 main states

 I managed to create a working Python program in short order, but when it came to making something similar with Visual Circuit I started facing some issues.

 A few were related to how i had initially placed the for loops and initialised nodes in my programs. After those were out of the way I faced an issue where overlapping commands were being sent to the motors.

 This was because the inbuilt abstraction over the motors used threading to keep supplying values, to deal with this i wrote my own publisher to the topic, it was quite simple and resolved the issue.

 Finally I had an issue where the bot could not go back to its initial state after getting to the third one.

 Unfortunately I couldn't resolve this within the week and had to push it forward as a part of next weeks goals

## Issues
No new Issues were raised this week
## Pull Requests
No new Pull Requests were issued this week however some corrections and updates were made on already active ones from the previous week.

<!---
 This leads me to a persistent question that developing with Visual Circuit is often harder than developing simply with Python... this needs to be solved in a meaningful way going forward.

 --->
---
layout: posts
title:  "Week 3: Coding Period"
date:   2022-07-10 12:08:00 +0530
categories: gsoc
---

## Major Tasks

### Template Updation
Continuing from where I left off last week, this week I finished all the remaining template blocks. A list of them would be Teleoperator, PID, MotorDriver, ObjectDetector, ROSCamera and Odometer. 

In addition, there were some improvements to be made to the old PR, that I had to update, namely I had included a Frequency constant in each of the blocks which wasn't needed anymore as the new version of Visual Circuit had the frequency directly built into the code block itself.

After updating that for all of the blocks once again I submitted the PRs.

### Read_String function

Currently Visual Circuit has functions to share arrays, images and numbers but no option to share strings. The other goal this week was to work with the backend of the application to add this feature.

In the process of adding this feature I discovered that the `read_number()` function would not work correctly either. 

The main problem was that the old version of the code would simply store the data from the Shared Memory Object in the wire. However when it came to access the wire a second time, the Shared Memory Object itself was not tracked hence it gave an error of leaked Shared Memory Object. 

To solve this, I stored the Shared Memory Object itself in the wire and while getting the data I simply got it from the buffer.

### Port Updation

THe old Visual Circuit used the port `80` for its backend to listen to. The problem with that was that `80` is a reserved port by the computer and required `sudo` access to be able to start a server on port `80`. 

To fix this I changed the port number that the backend listens on from `80` to `8000`

### Video Editing

Aside from this I also edited the videos made previously to make them more presentable. After a few iterations they were finally uploaded to the JdeRobot YouTube Channel. You can see the results below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/J1JhnNOKe1o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Xs3iAPYRtVQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Main t=changes were adding background music, some captions and speeding up some parts of the video.



## Issues
- [New Template blocks for remaining blocks](https://github.com/JdeRobot/VisualCircuit/issues/166)
- [read_number function in inputs doesn't work](https://github.com/JdeRobot/VisualCircuit/issues/164)
- [New template blocks OpenCV collection](https://github.com/JdeRobot/VisualCircuit/issues/161)
## Pull Requests
- [Update OpenCV Templates to the new Shared Memory Implementation](https://github.com/JdeRobot/VisualCircuit/pull/162)
- [Add read_string and share_string functions](https://github.com/JdeRobot/VisualCircuit/pull/165)
- [Update port used by backend from 80 to 8000](https://github.com/JdeRobot/VisualCircuit/pull/163)
- [Fix read_number function](https://github.com/JdeRobot/VisualCircuit/pull/167)
- [Update ROS Templates for new Shared Memory Implementation](https://github.com/JdeRobot/VisualCircuit/pull/168)
- [Update Control Templates for new Shared Memory Implementation](https://github.com/JdeRobot/VisualCircuit/pull/169)
- [Update Basic Code Template](https://github.com/JdeRobot/VisualCircuit/pull/170) 


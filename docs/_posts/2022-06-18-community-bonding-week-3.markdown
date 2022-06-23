---
layout: posts
title:  "Week 3: Community Bonding"
date:   2022-06-18 22:00:00 +0530
categories: gsoc
---

This was the last week of community bonding, however due to other commitments in college I had a hard time working on Visual Circuit.

The major work done this week consisted mainly of improving the solution to the Labyrinth Escape exercise.

I solved it using Visual Circuit as well, however due to a bug where string outputs weren't being transmitted between blocks the solution made using Visual Circuit was quite crude and didn't utilise blocks as well as it could have.

I also came up some ideas for new blocks that could be added to Visual Circuit:
- RQT block that open the vel-teleop and camera widget of Jde Drones
- IMU sensor 
- Differential drive controller
- Ultrasonic sensor [low priority]
- Block to open Rviz with or without a configuration loaded in

My mentors were pretty happy with my ideas, I was told to keep the Ultrasonic sensor at a lower priority as the implementation could prove difficult.
Since a lot of work was done on OpenCV blocks the last time around, there was a shift in focus towards ROS blocks
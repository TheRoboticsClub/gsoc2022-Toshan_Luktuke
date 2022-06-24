---
layout: posts
title:  "Week 1: Coding Period"
date:   2022-06-24 19:03:00 +0530
categories: gsoc
---

This week marked the official beginning of the coding period. Going by last week's set goals I started on the video creation part first and foremost.

In order to portray a Visual Circuit solution that was good to view as an example, I first had to solve a persistent bug that had troubled me for a while. 

Namely, I wasn't able to get string outputs to be shared between blocks. To solve this my mentor had suggested simply updating to a new version of the repo, I moved up a few commits and viola it worked as intended.

### Creating the Apps

Following that I started changing the old solutions that I had made to better utilise the **block design** of Visual Circuit. The diagrams of the solutions to Visual Lander and Labyrinth Escape are as follows:

![Visual Lander](/docs/_assets/visual_lander_diagram.png) 

![Labyrinth Escape](/docs/_assets/labyrinth_escape_diagram.png)

I noted a few bugs during this whole process namely:
- The files in staticfiles should be moved to the static folder
- Having multiple blocks of the same type causes them to be built with the same name e.g.:

![Multiple Blocks Bug](/docs/_assets/same_name_bug.png)

### Goals for Next Week
The main focus for next week will be on solving the issues encountered this week:
- Change between static and staticfiles (link to issue)
- Multiple same blocks are built incorrectly (link to issue)
- Improving block templates 

### Solution Videos

#### Visual Lander

#### Labyrinth Escape


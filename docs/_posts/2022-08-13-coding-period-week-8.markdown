---
layout: posts
title:  "Week 8: Coding Period"
date:   2022-08-13 23:55:00 +0530
categories: gsoc
---

I made more progress with the documentation and some other auxillary bug fixes this week.

## Documentation

Continuing on last week's images, this week I wrote the basic documentation for all of the blocks in Visual Circuit. 

It was done by adding a docstring to the `main()` function of the Python file. Pdoc then automatically reads it and displays it in an HTML format.

![Sample Documentation Page](/gsoc2022-Toshan_Luktuke/assets/sample_doc_page.png)

## FSM

We had a debugging session in the meet this week, however we couldn't find an efficient way to perfect the execution of the Vaccum Cleaner agent.

## Block Size

I discovered a bug that while saving blocks. Sometimes the height and width of the code blocks are saved as very small values roughly to the tune of 14-19px. So when loading a saved design again, the code block usually opens with a very small size. I pushed a commit fixing this issue in the existing blocks by changing their height and width values.

However, the larger symptom of why this bug occurs still remains at large.


## Adding .vc3 file to the built application

Aside from this I pushed a feature that added the `.vc3` configuration file to the built application as well. This is helpful as we often forget to save the configuration file while after building the application. Later if we want to make structural changes to our design, we will require this file. Hence bundling it along with the built application is more convenient for users.

## Issues 
- [Block Size is too small in certain cases](https://github.com/JdeRobot/VisualCircuit/issues/180)
## Pull Requests
- [Correct error in Threshold Block](https://github.com/JdeRobot/VisualCircuit/pull/179)
- [Add the .vc3 file to the built application](https://github.com/JdeRobot/VisualCircuit/pull/182)
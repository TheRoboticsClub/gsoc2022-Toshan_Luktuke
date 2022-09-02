---
layout: posts
title:  "Week 7: Coding Period"
date:   2022-08-06 12:08:00 +0530
categories: gsoc
---

Another pretty busy for me personally. This led to a bit of slowdown in the work done.

## Documentation

I started looking into extending and editing pdoc for our purposes. I found out that it had a customisable HTML template that could be edited easily using Jinja2.

I started learning about Jinja and after some time I could add the block images to the right hand side of the page made. 

![Blocks with Images](/gsoc2022-Toshan_Luktuke/assets/images_in_docs.png)

I did this by using the inbuilt svg code from the json file. I used it as a sort of dictionary depending on the page the user was on to display the image.




## FSM

I looked into what exactly was causing the weird behaviour in the FSM. In my opinion it was the multiprocessing aspect of the application with the control moving to different processes whenever a `sleep()` command was present.

To attempt a fix to this I used `Locks()` from Python's `multiprocessing` module. These Locks had to be added to the parameter list of the `main.py` file which is auto-generated. This allowed every module to inherit the lock as a part of its parameter list.

Yet, after using `lock.acquire()` and `lock.release()` in the critical section of the code, there was a huge difference in how the program executed.

The problems with different processes being started disappeared completely! 

## Pull Requests
No new Pull Requests were made this week
## Issues
No new issues were raised this week
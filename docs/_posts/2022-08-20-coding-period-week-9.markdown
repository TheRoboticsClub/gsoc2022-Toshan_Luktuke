---
layout: posts
title:  "Week 9: Coding Period"
date:   2022-08-20 23:55:00 +0530
categories: gsoc
---

This week saw the completion of the FSM video and the solution to the block size bug.

## Block Size
The problem lay in the fact that you don't have a resize event listener in HTML or React. Due to this Suhas made resize events fire using the onMouseDown listener in the block.

This caused the resize code to run whenever the user wrote code or typed in the block. This then set the size of the block to around 19px. 

To fix this, when firing re-size events we made the minimum size around 300px. While this isn't the best way to do it, it is still a fix until we think of some workaround.

## FSM Video
Suhas helped me again in this aspect. He tried to implement the FSM himself, in order to do that he added code that locked the processes execution while conducting input and output. This meant that only 1 process could write to the block at a time.

THis was very useful in implementing the sleep functions of the FSM. Using his modifications with my own code. The Vacuum Cleaner functioned the way it was intended to and I finished with the video. 

However, some editing is still remaining in the video and will be done soon.
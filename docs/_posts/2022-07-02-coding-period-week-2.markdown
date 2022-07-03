---
layout: posts
title:  "Week 2: Coding Period"
date:   2022-07-02 11:46:00 +0530
categories: gsoc
---

## Major Tasks

### Collectstatic
Going by the goals set last week and the advice of Suhas the first thing I did was to research the `collectstatic` step in the install.

It turns out that before we run the server we must first run `python3 manage.py collectstatic` what this does is that it collects all the files in the `staticfiles` folder and builds the `static` folder. This step was missing from the install instructions on both the repo and the website. So I added it to both the places.

### Multiple Blocks
Next was the issue where VisualCircuit built multiple blocks and gave them the same filename.

![Multiple Blocks Bug](/gsoc2022-Toshan_Luktuke/assets/same_name_bug.png)

To solve this I went into the `synthesis.py` file in the backend. Here I added a counter that kept track of how many of each type of block existed. Accordingly it appended a number like `1, 2, 3 ... etc.` to the end of the filename.

![Solved Bug](/gsoc2022-Toshan_Luktuke/assets/fixed_same_name_bug.png)

### Template Updation

Most of the time this week however went into the template updation work. After moving to the new shared memory implementation ([#151](https://github.com/JdeRobot/VisualCircuit/pull/151)) the old templates of the blocks needed to be updated.

E.g. of updated template for the Dilation Block:

![Blur Old Template](/gsoc2022-Toshan_Luktuke/assets/dilation_old.png)

![Blur New Template](/gsoc2022-Toshan_Luktuke/assets/dilation_new.png)

As you can see the new template is much simpler and easier to read. I majorly did all the OpenCV Blocks this week. They consist of about 60 - 65% of the blocks. The rest are to be done next week.

## Issues
Relevant Issues raised this week were:
- [Multiple Blocks have the same filename](https://github.com/JdeRobot/VisualCircuit/issues/157)
- [New template blocks OpenCV collection](https://github.com/JdeRobot/VisualCircuit/issues/161)
## Pull Requests
Relevant Pull Requests were:
- [Update Backend Install Instructions](https://github.com/JdeRobot/VisualCircuit/pull/156)
- [Fix the naming to be unique for each block](https://github.com/JdeRobot/VisualCircuit/pull/158)
- [Update OpenCV Templates to the new Shared Memory Implementation](https://github.com/JdeRobot/VisualCircuit/pull/162)

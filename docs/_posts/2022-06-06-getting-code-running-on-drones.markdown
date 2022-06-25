---
layout: posts
title:  "Getting Code Running on Drones"
date:   2022-06-06 13:16:00 +0530
categories: gsoc
---

After I got the drones running now it was time to actually write the code to solve some exercises. The goal for this week of the GSoC
period was to get 1-2 applications of the drones solved using Visual Circuit.

But before I could do that, I had to get my code to run on the drones.

### Running the Scripts

The way JDE Drones works is that we have a widget that allows us to control most aspects of the drone. ![Drones Widget](/docs/assets/drones-widget.png)

What we have to do is write our code in the `my_solution.py` file 

![Example of file structure](/docs/assets/my_solution_file.png)

and click on the `Play Code` button after takeoff of the drone to run our code.

This worked well enough for the exercises, `drone_gymkhana`, `follow_road` and `drone_hangar` when I tested them. However a problem arose in the exercise `drone_cat_mouse`. The problem was that the widget itself did not appear when the exercise was launched.

### Problem and Solution

When this happened I was quite confused. Since all of my other exercises were working properly I had come to the conclusion that all of my installs were done correctly. In this case I had no idea what exactly was going wrong, I got a hint by using `rostopic echo`. The output consisted of topics that were pre-fixed by `cat/` or `mouse/`, for each drone respectively. ![Rostopic output](/docs/assets/cat_mouse_rostopic_list.png)

The difference here was that each drone had the namespace prefixed to its topic. The namespace was `cat/` or `mouse/`. When initializing the `DroneWrapper()` class in `my_solution.py` we had to pass the namespace to the class as a parameter.

```python
# DroneWrapper(node_name, namespace)
HAL = DroneWrapper('drone','cat/') 
```
The above code was what I needed to get the `my_solution.py` file to execute. 

I'm still thinking of a solution to get the widget working. One way is to go into the `drone_vel_teleop` class manually and set the default namespace as `cat/`. However this isn't really a long term solution to the problem.

This blog will be updated if I find a way to get the widget working well. For the time being however my current method is enough to solve the exercise.

---
layout: posts
title:  "Week 4: Coding Period"
date:   2022-07-17 12:19:00 +0530
categories: gsoc
---

This week marked a focus on completing the remaining PRs from last week. I also finished adding a new IMU block and worked on general `share()` and `read()` functions.

### IMU Block

An IMU (Inertial Measurement Unit) is a sensor commonly found in drones that detects the orientation and the angular velocities of the robot.

It is essential for writing our own control systems for drones. I started the work on the block. For testing how it worked I used the `visual_lander` simulation. Since mavros already has an inbuilt IMU in its models. Constructing the block template was just about reading the processing the data already gotten in an appropriate manner. 

![IMU Block](/gsoc2022-Toshan_Luktuke/assets/imu_block.png)

The code is as follows:
```python
import numpy as np
import rospy
from sensor_msgs.msg import Imu
from tf.transformations import euler_from_quaternion

data = []

def callback(msg):
    global data
    # Get the orientation list from the IMU sensor
    orientation_list = [msg.orientation.x,msg.orientation.y,msg.orientation.z,msg.orientation.w]
    # Convert orientation obtainted into values of roll, pitch and yaw
    (roll,pitch,yaw) = euler_from_quaternion(orientation_list)
    # Convert val;ues in Radians to Degrees
    roll = roll * (180/3.14159265)
    pitch = pitch * (180/3.14159265)
    yaw = yaw * (180/3.14159265)
    # Obtain Angular Velocities from IMU sensor
    angVel_x = msg.angular_velocity.x
    angVel_y = msg.angular_velocity.y
    angVel_z = msg.angular_velocity.z
    # Store all this data in 'data' variable for use in main function
    data = [roll, pitch, yaw, angVel_x, angVel_y, angVel_z]
    # ----- Lines only for demo purpose -----
    rospy.loginfo("Orientation\nRoll = {0}\nPitch = {1}\nYaw = {2}\n".format(roll,pitch,yaw)) # These are not included in the block's code
    rospy.loginfo("Angular Velocities\nWx = {0}\nWy = {1}\nWz = {2}\n".format(angVel_x,angVel_y,angVel_z)) # These are not included in the block's code

def main(inputs, outputs, parameters, synchronise):
    global data 
    auto_enable = False
    try:
        enable = inputs.read_number('Enable')
    except Exception:
        auto_enable = True

    rospy.init_node('imu_vc')
    rostopic_name = parameters.read_string("ROSTopic")
    rospy.Subscriber(rostopic_name, Imu, callback)

    while ((auto_enable or inputs.read_number('Enable')) and not rospy.is_shutdown()):
        if not data:
            continue

        outputs.share_array("Out", data)
        synchronise()
```

And the output:

![IMU Output](/gsoc2022-Toshan_Luktuke/assets/imu_data.png)

### General Share and Read
The other major task done this week was creating a general read and share function. Before this in Visual Circuit we had separate functions to share the output of blocks. 

For e.g. in order to share an image we had to write `share_image(...)`, similarly for an array `share_array(...)` and on the other end to read then we had to include specific functions such as `read_image(...)` and `read_array(...)` as well. 

This was something that could be improved to make it simpler for the users. 
The reason this was done separately was that while sharing something we have its data type, hence it can be general purpose, however while reading it we don't know what kind of data type we'll be getting hence the need for specific functions. We need the exact data type while reading because when the Shared Memory Buffer is read it is specific for the supplied data type.
---
layout: post
title:  "ROS and ROS-MoveIt!"
date:   2015-09-01 10:13:42
categories: projects
image: images/moveit.png
---

In our second Robotics & Vision project, we were working on a pick & place task.
The goal was to estimate the pose of a known object, grab it with a robotic
arm and place it into a bin. Our workcell consisted of a 7-dof Mitsubishi PA-10
robotic arm and a RGB-D camera for pose estimation. For implementing pose estimation
and path planning, we were encouraged to use OpenCV, ROS and the university's
own robotics library [Robwork][robwork].

However, since we made bad experience with Robwork in the previous project, we
decided to go with another framework, namely [ROS-MoveIt!][moveit]. MoveIt! is a
state of the art and easy to use robotic software and we never regretted choosing
it. However, there were two major drawbacks compared to using Robwork:

1. The PA-10 was not supported by MoveIt!
2. There was no interface to the PA-10 controller which translates the planned trajectory to a robot movement

Luckily we found a collada file of a PA-10 on the internet, which allowed us to
create a URDF (Universal Robot Description File) for the PA-10. This file
contains all the joint and link dimensions and is used by MoveIt! to calculate all
necessary transformations for forward and inverse kinematics → Planning. Once we had the
URDF ready, we could import it into the ROS visualization tool RVIZ and do some
simulated planning and execution in our virtual workcell. We used the simulator
of ros-industrial for the simulation.

The next step was to integrate the PA-10 controller into MoveIt!, so we could
control the robotic arm via the RVIZ MoveIt! plugin. It took some time reading
the MoveIt and PA-10 controller documentation (which were quite bad at that time)
but I finally got a python script running which published the PA-10 joint states
as a ROS-topic so they could be processed by MoveIt!. It was a great feeling
controlling the PA-10 manually and simultaneously seeing the robot move in RVIZ
accordingly. A second "translator script" was used to translate the MoveIt! trajectories into
ROS sevice calls for the PA-10 controller.

For this project I had to dig very deeply into ROS and ROS-MoveIt! and thereby got to know
it very well. It's a great piece of software and I really enjoy working with it.
The source code of our PA-10 adaptions including *PA10_descreption* and *PA10_moveit_config*
can be found at my [Bitbucket repository][bitbucket].

[robwork]:      http://www.robwork.dk/jrobwork/
[moveit]:   http://moveit.ros.org/
[bitbucket]: https://bitbucket.org/akrauch/rovi2_group8

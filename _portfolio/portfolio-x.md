---
title: "Interactive Robotic Vacuum"
excerpt: "SNU Creative Design Fair <br/><img src='/images/InteractiveRobot.png' align='middle' width='700' height='500'>"
collection: portfolio
---
<br><br>

<img src='/images/InteractiveRobot.png' align='middle' width='1000' height='700'>

<p style="text-align:justify;">

I participated in 2020 Creative Desgin Fair as a team of four. 2020 Creative Desgin Fair was a competition held by the college of Engineering in Seoul National University, where participating teams competed with creativity and ability to implement. Our team implemented an Interactive Robotic Vacuum with a novel shape & locomotion. Our work has three unique features: 1) a unique pointed body shape, 2) mecanum wheels, and 3) a smart phone application with hand gesture detection model. My role was implementing the algorithm for the automatic control, and implementing the smartphone application for human-robot interaction (HRI). I was also heavily involved in building the robot body from scratch. Our team won the 2nd place of the competitoin. <br><br>

As the ornidanry vacuums have round shapes and inlets on their ventral side, they cannot sweep the inside of corners perfectly. Unlike other ordinary robotic vacuums, our robot has a pointed shape body, where the vacuum inlet is on a side of the tip allowing the robot to sweep corners scrupulously. <br><br>

However, due to the position of the inlet, the sweeping area of the robot is not same as the trajectory of the robot. Therefore, in terms of controlling robot, we need to consider not only the locomotion of the robot, but also the head direction of it. To tackle this, we equippe the robot with mecanum wheels, a.k.a omnidirectional wheels, which have a better freedom of maneuverability. With mecanum wheels, the robot is able to change its instantaneous center of rotation (ICR) flexibly, and by dynamically adjusting ICR, the robot can sweep any kinds of convex  concave shapes of walls with its tip. <br><br>

The control system was implemented on an Arduino board and a RPLiDAR was used for sensing topographical features (e.g. walls, obstacles). The rotating laser sensor in RPLiDAR produces distance from any obstacle in all directions. A coarse grained egocentric map was implemented with the sensor data, which is used to determine the situation of the robot (e.g. confronting obstacle or incoming corner). Given the map, a simple rule based algorithm automatically controls the robot to sweep a flat wall or a corner. <br><br>

The lack of interaction with robots is one of the major sources of users' low confidence in robots. Our team devised a novel HRI platform where users can interact with the robot by hand gestures. As the core of the platform, a smart phone application detects user's hand gesture and send commands to the robot according to the detected gesture. The hand gesture detector was implemented using MediaPipe, an open source package developed by Google. We also utilized the pretrained hand tracking model provided from the package developers. As a proof of concept, we implemented an application which moves the robot to be aligned with users hands position. This allows users to control the robot with their hands, and clean the floor with sweeping gesture. <br><br>





</p>


Reference <br><br>

[1] 

---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "Jekyll, Pineapple"

project:
  title: "BotChoco"
  type: "Jekyll"
  url: "https://github.com/arnolds/BotChoco"
  logo: "/assets/images/projects/redpineapple/logo.png"
  tech: "HTML, CSS, Boostrap, Sass, JavaScript, jQuery, Jekyll"

images:
  - image:
    url: "/assets/images/projects/redpineapple/devices.jpg"
    alt: "Red Pineapple website on tablet, mobile and desktop"
  - image:
    url: "/assets/images/projects/redpineapple/desktop.jpg"
    alt: "Red Pineapple website on a desktop device"
  - image:
    url: "/assets/images/projects/redpineapple/mobile.jpg"
    alt: "Red Pineapple website on a mobile device"
---

X6 speed 

## Technologies
Ros, Python, OpenCV, Manipulation

## Project
In this project, a Franka Emika Panda robot arm was programmed to autonomously make a cup of hot chocolate.


Given a kettle, a cup, a stirrer and a scoop with chocolate powder, the robot is able to turn on the kettle, pour the chocolate powder into the cup, pour the hot water into the cup, and stir to make the hot chocolate fully dissolved.

In this project, my major role was to implement computer vision pipeline with other teammates that accurately detects the location of each object in the work space, design and fabricate physical supports for robot to interact with objetcs, create a obstacle generation function to allow robot avoid collision with other objects in the work space.

In the conputer vision pipeline, a RGB video stream is provided by an Intel Realsense D435i camera. The video allows the objects to be located in the work space by the related AprilTags. The camera frame is linked with robot base frame. The relationship is provided by calibration through an AprilTag temporary attached to the end effector. This allows the camera frame and detected object frame linked with robot frames. Two AprilTags are used to represent the objects' location. One tag is for the kettle and another one is for the jig which is used to set cup, scoop, and stirrer. Because of the jig, the frames for cup, scoop, and stirrer can be converted from a single AprilTag without  In this case, all the objects are linked with robot frame through the the conputer vision pipeline which can be easily accessed by robot control package.

Before making coffee, if the camera is moved, a calibration is required to rebuild the transformation frame between camera and robot. When the program is started, the computer vision pipeline provides the object frame infomation to robot and update the infomation if the object is not located at the original location. 

The obstacle adding function can provide possible collision space for the robot. This allow the robot to positively avoid collision with objects in the working space during path planning.

The final results show the program is able to successfully make hot chocolate with high rates of success. Future work may involve adding machine learning object detection and kettle status detection.

My primary role in this project was to design and implement the perception pipeline that senses where tools are located, the pancake location to assist with flipping & lifting the pancake, and autonomously determining when the pancake should be flipped.


The perception pipeline begins with an Intel Realsense D435i camera, which provides an RGB-D image. This depth data allows the pancake to be found using OpenCV contour recognition, in 3-Dimensions relative to the camera. The camera's coordinate frame (and the coordinate frames of the bottle and spatula) is linked to the robot's coordinate frame via an AprilTag a fixed distance from the robot base. The tools are located via AprilTags as well, provided the tag is visible the pipeline is able to determine the 6-DOF pose of the AprilTag without any depth data. This provides additional resilience towards varying backgrounds, lighting, and other camera issues. From the linked transformation tree, the perception pipeline is able to determine the locations of the tools and pancake in the robot's frame, eliminating the need for visual servoing and simplifying path planning


Flipping a pancake with chocolate chips
An overhead view of the workspace, tools, and AprilTags for object identification.

Once the pancake is put onto the griddle, the perception pipeline aims to determine an appropriate time to flip the pancake much like a human would. By counting the contours on the griddle's surface, the program is able to determine the number of bubbles that appear on the pancake's surface. Empirical testing shows that for the pancakes created by the squeeze bottle, the number of bubbles rises, plateaus, and declines around the right time to flip - when the robot then moves to pick up the spatula.


This perception pipeline is integrated into ROS Noetic, which controls the arm using the MoveIt! control package. Motion planning is accomplished by specifying a target pose and using the RRT (Rapidly-exploring Random Tree) planner in OMPL (Open Motion Planning Library) to plan a set of joint states that bring the robot to the pose while abiding by planning scene constraints (the table, the camera, etc). The motion planning is aided by preprogrammed waypoints for the end effector pose and collision objects in RViz, to guarantee that the planner took an appropriate path


Final results yield a program that is able to successfully make pancakes with high rates of success. Future work may involve adding toppings, or flipping the pancake in the air with a frying pan rather than a spatula.
---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "ROS, Computer Vision, Robotic Manipulation"

project:
  title: "Robotic Pancake Chef"
  type: "Jekyll"
  url: "https://github.com/javtges/robot-pancake-chef"
  logo: "/assets/images/projects/pancake/pancake_flip.jpg"
  tech: "ROS, Python, OpenCV, MoveIt"


images:
  - image:
    url: "/assets/images/projects/pancake/IMG_6158.jpg"
    alt: "An overhead view of the robot"
  - image:
    url: "/assets/images/projects/pancake/pancake_flip2.jpg"
    alt: "Flipping a pancake with chocolate chips"
  - image:
    url: "/assets/images/projects/pancake/pancake_flip.jpg"
    alt: "A finished pancake deposited onto a plate"
---


<p>In this project, a final course project for ME495 - Embedded Systems in Robotics, a Franka Emika Panda robot arm was programmed to auntonomously cook pancakes.


<br><br>Given a spatula and a bottle of pancake batter, the robot is able to manipulate the tools, flip the pancake, and serve it onto a plate.


<br><br>My primary role in this project was designing and implimenting the perception pipeline that senses where tools are located, the pancake location to assist with flipping & lifting the pancake, and auntonomously determining when the pancake should be flipped.


<br><br>The perception pipeline begins with an Intel Realsense D435i camera, which provides an RGB-D image. This depth data allows the pancake to be found using OpenCV contour recognition, in 3-Dimensions relative to the camera. The camera's coordinate frame is linked to the robot's coordinate frame via an AprilTag a fixed distance from the robot base. The tools are located via AprilTags as well, provided the tag is visible the pipeline is able to determine the 6-DOF pose of the object without any depth data.


<br><br>Once the pancake is put onto the griddle, the perception pipeline begins counting the bubbles that appear on the pancake's surface, much like a human would determine when it's time to flip the pancake.


<br><br>This perception pipeline is integrated into ROS Noetic, which controls the arm using the MoveIt! control package. Motion planning is accomplished by specifying a target pose and using an RRT to plan a set of joint states that bring the robot to the pose while abiding by planning scene constraints (the table, the camera, etc).


<br><br>Final results yield a program that is able to successfully make pancakes auntonomously with high rates of success. Future work may involve adding toppings, or flipping the pancake in the air with a frying pan rather than a spatula.</p>
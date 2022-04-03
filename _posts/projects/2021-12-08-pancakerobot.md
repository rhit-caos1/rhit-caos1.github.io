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


<!-- <p>In this project, a Franka Emika Panda robot arm was programmed to auntonomously cook pancakes.</p>
<br>
<p>Given a spatula and a bottle of pancake batter, the robot is able to manipulate the tools, flip the pancake, and serve it onto a plate.</p>
<br>
<p>My primary role in this project was designing and implimenting the perception pipeline that senses where tools are located, the pancake location to assist with flipping & lifting the pancake, and auntonomously determining when the pancake should be flipped.</p>
<br>

<p>The perception pipeline begins with an Intel Realsense D435i camera, which provides an RGB-D image. This depth data allows the pancake to be found using OpenCV contour recognition, in 3-Dimensions relative to the camera. The camera's coordinate frame is linked to the robot's coordinate frame via an AprilTag a fixed distance from the robot base. The tools are located via AprilTags as well, provided the tag is visible the pipeline is able to determine the 6-DOF pose of the object without any depth data.</p>
<br>

![test image](/assets/images/projects/pancake/pancake_flip.jpg)

<p>Once the pancake is put onto the griddle, the perception pipeline begins counting the bubbles that appear on the pancake's surface, much like a human would determine when it's time to flip the pancake.</p>
<br>

<p>This perception pipeline is integrated into ROS Noetic, which controls the arm using the MoveIt! control package. Motion planning is accomplished by specifying a target pose and using an RRT to plan a set of joint states that bring the robot to the pose while abiding by planning scene constraints (the table, the camera, etc).</p>
<br>

<p>Final results yield a program that is able to successfully make pancakes auntonomously with high rates of success. Future work may involve adding toppings, or flipping the pancake in the air with a frying pan rather than a spatula.</p>
<br> -->

---
layout: post
title: "The Adventures of Sherlock Holmes"
---

"But if he is innocent, who has done it?"

"Ah! who? I would call your attention very particularly to two points. One is that the murdered man had an appointment with someone at the pool, and that the someone could not have been his son, for his son was away, and he did not know when he would return. The second is that the murdered man was heard to cry 'Cooee!' before he knew that his son had returned. Those are the crucial points upon which the case depends. And now let us talk about George Meredith, if you please, and we shall leave all minor matters until to-morrow."

There was no rain, as Holmes had foretold, and the morning broke bright and cloudless. At nine o'clock Lestrade called for us with the carriage, and we set off for Hatherley Farm and the Boscombe Pool.

"There is serious news this morning," Lestrade observed. "It is said that Mr. Turner, of the Hall, is so ill that his life is despaired of."

"An elderly man, I presume?" said Holmes.

"About sixty; but his constitution has been shattered by his life abroad, and he has been in failing health for some time. This business has had a very bad effect upon him. He was an old friend of McCarthy's, and, I may add, a great benefactor to him, for I have learned that he gave him Hatherley Farm rent free."

"Indeed! That is interesting," said Holmes.

"Oh, yes! In a hundred other ways he has helped him. Everybody about here speaks of his kindness to him."
---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "Deep Learning, Computer Vision, Pytorch"

project:
  title: "Deep Learning for Gesture Recognition"
  type: "Jekyll"
  url: "https://github.com/javtges/"
  logo: "/assets/images/projects/gesture/fist_gesture.png"
  tech: "Deep Learning, Computer Vision, Pytorch"


images:
  # - image:
  #   url: "/assets/images/projects/pancake/IMG_6158.jpg"
  #   alt: "An overhead view of the robot"
  # - image:
  #   url: "/assets/images/projects/pancake/pancake_flip2.jpg"
  #   alt: "Flipping a pancake with chocolate chips"
  # - image:
  #   url: "/assets/images/projects/pancake/pancake_flip.jpg"
  #   alt: "A finished pancake deposited onto a plate"
---


<p>Gestures are a common and especially alluring method of human-computer interaction. For decades media has depicted science-fictional computer wizards manipulating computers and robots with a swipe of a hand, as if a digital interface was tangible and could be grabbed and dragged about.
<br>
However, in practice, dynamic gesture recognition is a surprisingly difficult task, which I approach in this project. Starting as a total beginner in deep learning, I experimented with and implimented multiple common methods of recognizing dynamic hand gestures.</p>
<br>


<p>Time-series data struggles with a fundemental challenge in live inference tasks - that is, the problem of segmentation. In a live video stream, there's no definite beginning or end of the gesture, and the time the gesture takes to be performed can be variable.
<br>
Various solutions to this temporal classificaion problem exist in the deep learning space, most prominently recurrent neural networks (RNNs) which take multiple inputs - a more traditional input for a CNN layer, and a previous state of the RNN. This is used in models such as LTSMs, and specific loss functions have been developed for use with these networks, such as CTC: Connectionist Temporal Classification loss.</p>
<br>


<p>My primary role in this project was designing and implimenting the perception pipeline that senses where tools are located, the pancake location to assist with flipping & lifting the pancake, and auntonomously determining when the pancake should be flipped.</p>
<br>

<p>The perception pipeline begins with an Intel Realsense D435i camera, which provides an RGB-D image. This depth data allows the pancake to be found using OpenCV contour recognition, in 3-Dimensions relative to the camera. The camera's coordinate frame is linked to the robot's coordinate frame via an AprilTag a fixed distance from the robot base. The tools are located via AprilTags as well, provided the tag is visible the pipeline is able to determine the 6-DOF pose of the object without any depth data.</p>
<br>

<p>Once the pancake is put onto the griddle, the perception pipeline begins counting the bubbles that appear on the pancake's surface, much like a human would determine when it's time to flip the pancake.</p>
<br>

<p>This perception pipeline is integrated into ROS Noetic, which controls the arm using the MoveIt! control package. Motion planning is accomplished by specifying a target pose and using an RRT to plan a set of joint states that bring the robot to the pose while abiding by planning scene constraints (the table, the camera, etc).</p>
<br>

<p>Final results yield a program that is able to successfully make pancakes auntonomously with high rates of success. Future work may involve adding toppings, or flipping the pancake in the air with a frying pan rather than a spatula.</p>
<br>
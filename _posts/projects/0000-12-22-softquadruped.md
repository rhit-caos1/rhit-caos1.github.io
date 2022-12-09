---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "Soft Robotics, Reinforcement Learning"

project:
  title: "Reinforcement Learning for Soft Robots"
  type: "Jekyll"
  url: "https://github.com/javtges/soft_quadruped"
  logo: "/assets/images/projects/final/hsa_robot.jpg"
  tech: "Soft Robotics, Reinforcement Learning"
---



<!-- Add some links here to their bios / labs -->
<p>This is my MSR Final Research Project! It was conducted in the Spring and Fall quarters of 2022, within Northwestern's <a href="https://sites.northwestern.edu/roboticmatterlab/" target="_blank"><u>Robotic Matter Lab</u></a>. 
I had the incredible fortune to be advised by Professors <a href="https://www.mccormick.northwestern.edu/research-faculty/directory/profiles/truby-ryan.html" target="_blank"><u>Ryan Truby</u></a> 
and <a href="https://robotics.northwestern.edu/people/profiles/faculty/elwin-matt.html" target="_blank"><u>Matthew Elwin</u></a>, and to collaborate with Professor
<a href="https://www.mccormick.northwestern.edu/research-faculty/directory/profiles/murphey-todd.html" target="_blank"><u>Todd Murphey's</u></a> lab.</p> 


<!-- Maybe put a picture here again of the robot, cover art for Soft Matter? -->
<br>

### Background: Gait Optimization for Soft Systems

<p>In this project, I am working with a soft-legged quadruped, with legs composed of Handed Shearing Auxetics (HSAs). 
  These are flexible 3D printed structures with a negative Poisson's ratio, expanding and contracting when subjected to rotation. 
We print HSAs out of polyurethane-like material, using stereolithography.</p>

<br>

<p>An HSA is composed of two of these auxetic cylinders. When paired together, two HSA pairs can create a structure that can expand, contract, bend, and twist.</p>
<br>
<!-- put a picture here of an HSA -->

<p>I joined the Robotic Matter Lab when Pranav Kaarthik was working with HSAs to create an quadruped. Using a hand-defined gait, he demonstrated untethered locomotion for over an hour, while carrying a payload of 1.5kg. 
  This work appeared in "Motorized, untethered soft robots via 3D printed auxetics", accepted to <i>Soft Matter</i> in the Fall, and was the cover art for a themed collection on soft robotics!
</p>
<br>

<p>My research builds upon this foundation, establishing reinforcement learning methods applicable to such a system - with the goal of learning an optimized gait that improves the robot's walking speed.</p>
<br>

### Challenges in Controlling Soft Systems

<p>Soft robotics exhibit potential for safe human-robot interaction, operation in hazardous places, and more. However, their compliance, the very property that provides such benefit, is also a major challenge in controlling them.
  In the particular example of an HSA robot, the forward kinematics are unknown - the relationship between motor commands and leg displacement is unintuitive, and is further complicated by the compliant nature of the structures.
</p>
<br>
<p>Additionally, as soft robots rely on material deformation to move, the lifespan of soft actuators is by definition limited by its material properties. This leads to actuation properties that vary over time.
</p>
<!-- put a picture here of a broken HSA -->
<br>

### Initial Approach: Online Policy Gradient Estimation

<p>These challenges led to a first attempt at reinforcement learning for such a system  - online policy gradient estimation, with methods derived from PETER STONE PAPER.
  The intention for this method is to use the simplest learning architecture possible, and avoid the complexities of modeling & simulating such a complex dynamical system.
</p>
<br>

<!-- Throw in peter stone block diagram -->

<p>Here, I parameterized the values in the hand-tuned policy, while preserving the gait's structure. However, it was found that given the parameter space we were searching, the system was very brittle with respect to parameter
  perturbations. While it is certainly possible to have learned a more optimal gait using this method (<i>and should I have had more time, I would've loved to explore further!</i>), the timescales required (<i>and therefore the number of motors and HSAs printed</i>) was prohibitive. Thus, I led the initiative to pivot to a sim-to-real approach to learn gaits on this system.
</p>
<br>

### Creating a Simulation Environment

### Policies Modulating Trajectory Generators

### Test Fixturing to Capture Dynamics

### Sim-to-Real Transfer

<br>


<br><br>


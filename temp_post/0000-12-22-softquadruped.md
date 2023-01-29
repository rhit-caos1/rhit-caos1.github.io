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

<br>

![Soft Matter Cover](/assets/images/projects/final/hsa_robot_beach.png)
<center><h2>Cover photo from a themed collection on soft robotics, <i>Soft Matter</i></h2></center>


<br>

### Background: Gait Optimization for Soft Systems

<p>In this project, I am working with a soft-legged quadruped, with legs composed of Handed Shearing Auxetics (HSAs). 
  These are flexible 3D printed structures with a negative Poisson's ratio, expanding and contracting when subjected to rotation. 
We print HSAs out of polyurethane-like material, using stereolithography.</p>

<br>

<p>An HSA is composed of two of these auxetic cylinders. When paired together, two HSA pairs can create a structure that can expand, contract, bend, and twist.</p>
<br>

<!-- put a picture here of an HSA -->
<!-- ![HSA Movements](/assets/images/projects/final/hsa_robot_movements.png) -->
<img class="img80" src="/assets/images/projects/final/hsa_robot_movements.png" width="1200"> 
<center><h2>Kaarthik et al., “Motorized, untethered soft robots via 3D printed auxetics”, <i>Soft Matter</i>, 2022.</h2></center>

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

<p>These challenges led to a first attempt at reinforcement learning for such a system  - online policy gradient estimation, with methods derived from <a href="https://www.cs.utexas.edu/~pstone/Papers/bib2html-links/icra04.pdf" target="_blank"><u><i>Policy Gradient Reinforcement Learning for Fast Quadrupedal Locomotion</i></u></a>, one of the earliest examples of learned legged locomotion from 2004.
  The intention for this method is to use the simplest learning architecture possible, and avoid the complexities of modeling & simulating such a complex dynamical system.</p>
<br>

<!-- Throw in peter stone block diagram -->
![Peter Stone Block Diagram](/assets/images/projects/final/peterstone.png)
<center><h2>Nate Kohl and Peter Stone, “Policy Gradient Reinforcement Learning for Fast Quadrupedal Locomotion”, ICRA, 2004.</h2></center>

<p>Here, I parameterized the values in the hand-tuned policy, while preserving the gait's structure. However, it was found that given the parameter space we were searching, the system was very brittle with respect to parameter
  perturbations. While it is certainly possible to have learned a more optimal gait using this method (<i>and should I have had more time, I would've loved to explore further!</i>), the timescales required (<i>and therefore the number of motors and HSAs printed</i>) was prohibitive. Thus, I led the initiative to pivot to a sim-to-real approach to learn gaits on this system.
</p>
<br>

<!-- Picture of Peter Stone results -->
<!-- ![Online Learning Results](/assets/images/projects/final/stone_results.png) -->
<img class="img80" src="/assets/images/projects/final/stone_results.png"> 
<center><h2>Results on a per-trial basis, using online policy gradient RL</h2></center>
<br>

### Creating a Simulation Environment

<p>I created a simulation environment based off of Pybullet, and made it compatible with OpenAI's Gym workflow, a useful framework for reinforcement learning tasks. The robot modeled in simulation, is defined by a URDF with two joints: a revolute and prismatic joint connected together.</p>

<br>

<!-- Add a gif here of the robot moving its 'hips' around -->
![HSA Robot Moving in Pybullet](/assets/images/projects/final/hsa_pybullet_joints.gif)
<center><h2>HSA Robot, in Pybullet, moving its joints around</h2></center>

### Policies Modulating Trajectory Generators

<p>To learn a gait in simulation, I use the architecture <a href="https://arxiv.org/abs/1910.02812" target="_blank"><u><i>Policies Modulating Trajectory Generators</i></u></a>. This allows the agent to learn a policy for a gait like more 'conventional' reinforcement learning, but allows
  some prior knowledge to be added to bootstrap the simulation. It takes the form of a periodic Trajectory Generator, which in the original paper, defines the path in space that a robot's foot follows. It's defined by various
  parameters, which are learned by the policy given an observation.
</p>
<br>
<p>The policy learns additional values, too, residual values that allow the policy to modulate the Trajectory Generator's output based on an observation (Euler angles, in this case). In the original and my implementation, it takes the form of X and Y
  offsets for each leg. It also learns a <i>time offset</i> value - which modulates the phase of each leg, transitioning the Trajectory Generator into a general-purpose point selection set for each timestep within the simulation.
</p>

<!-- add PMTG architecture block diagram -->
![PMTG Block Diagram](/assets/images/projects/final/pmtg_block.png)
<center><h2>Iscen et al., “Policies Modulating Trajectory Generators”, Conference on Robot Learning (CoRL), 2018.</h2></center>


<p>In order to improve the sim-to-real transfer effectiveness, I apply Gaussian noise to each set of simulation inputs, along with applying domain randomization for each rollout, increasing the robustness of the policy.
  Many implementation details are inspired by <a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9636011" target="_blank"><u><i>Linear Policies are Sufficient to Enable Low-Cost Quadrupedal Robots to Traverse Rough Terrain</i></u></a>, where the application of residuals, gait time dilation, and domain randomization is
  critical to enable a rigid quadruped to walk and "stumble" through rough terrain without falling over.
</p>
<br>

<p>Following this paper, I also implement a simple linear policy rather than a more complex neural network-based architecture, and use <a href="https://arxiv.org/pdf/1803.07055.pdf" target="_blank"><u>Augmented Random Search</u></a> to train it. It trains in minutes on CPU, and converges on the order of only hundreds of rollouts.
</p>
<br>


### Test Fixturing to Capture Dynamics

<p>In order to enable sim-to-real transfer, I need to tackle the challenge of forward kinematics for the HSA quadruped. I chose to accomplish this in a computationally-efficient way possible, a simple lookup table to approximate the complex mapping
  between motor inputs and HSA displacement.
</p>
<br>

<p>Furthermore, to match the simulation, I constrain leg movement to planar extensions, contractions, and bending. Due to the handed nature of the legs, it means that a given HSA position can be represented by two motor commands,
  rather than four. Our servos that actuate the HSAs move approximately 180 degrees, so when considering 90 degrees as a nominal value, the parameter vector of motor inputs for each leg ends up being <code>[M, 180-M, N, 180-N]</code>.
</p>
<br>

<p>To simulate compliant behavior of the robot's legs under loading conditions similar to walking, I designed a test fixture for a single leg. Preloaded springs on each corner provide a constant force similar to one-quarter
  of the robot's expected weight, and allow the leg to contract without any resistive force. Extending the leg applies more force to "push the robot up".
</p>
<br>

<!-- a picture of the test fixture -->
![HSA Test Fixture](/assets/images/projects/final/hsa_cage.png)
<center><h2>Test fixture for capturing HSA dynamics</h2></center>

<p>Using an AprilTag, I then perform a set of planar sweeps to cover the parameter space for the leg. It results in a lookup table as shown below - each dot represents a combination of motor commands and the inplane displacement of the leg from the origin <code>(0,0)</code>, when the motors are at their neutral location. 
  In the full lookup table, compiled over multiple hours and ~12 complete inplane sweeps covering the parameter space, it's visually apparent that <strong>1.</strong> the HSA properties remain reasonably consistent over time, and <strong>2.</strong> HSA displacement at a given set of motor values is reasonably
  repeatable, regardless of the actuator's strain rate or direction of movement. The resulting dimensions of the lookup table then define the joint limits in the simulation's URDF file.
</p>
<br>
<!-- GIF / image of the lookup table -->


| Animated Lookup Table  | Full Lookup Table |
| ------------- | ------------- |
| <img class="img80" src="/assets/images/projects/final/lut_animation.gif">  | <img class="img80" src="/assets/images/projects/final/interpolate_lut.png">  |


<p>Finally, I perform bilinear interpolation to go from an arbitrary set of XY values in the leg's coordinate frame, to a set of motor commands that most closely replicate it. Appending this to the end of the PMTG pipeline allows translation of simulated policies into real life.</p>
<br>

![HSA Test Fixture](/assets/images/projects/final/full_diagram.png)
<center><h2>The full system diagram for running a policy on a real robot</h2></center>

<br>

<!-- Add image of interpolation if I have time -->



### Learning and Optimizing Gaits - in Simulation and Real Life

<p>At long last, we're ready to perform sim-to-real transfer. Using bilinear interpolation, I demonstrated an elliptical gait - not learned, though derived from my lookup table - that exceeds the hand-tuned gait speed
  demonstrated in <i>Soft Matter</i> by ~25%.
</p>
<br>

![HSA Robot Moving in Pybullet](/assets/images/projects/final/default_gait_slow.gif)
<center><h2>Closed-loop circular gait in Pybullet</h2></center>


<!-- Video of robot walking quickly -->
![HSA Robot Moving in Pybullet](/assets/images/projects/final/hsa_circle_gait.gif)
<center><h2>Closed-loop circular gait in real life</h2></center>


<p> This is corroborated in the simulation results, where we can observe the robot learning significantly in only hundreds of rollouts, sometimes fewer. Initial results showed nearly 5x improvement in gait speed, largely
  due to the "time-warping" functionality of the policy, effectively walking far faster than the zero policy gait.
</p>
<br>

<img class="img80" src="/assets/images/projects/final/hsa_fastwalk.gif"> 
<center><h2>Time modulation allows quicker leg movements</h2></center>

<!-- Video of robot starting out walking, and then video of robot walking FAST -->
<p>However, this type of gait isn't reasonable to run on the real robot - the HSAs don't move this fast in real life. Therefore, current work focuses on slowing down gaits while still generating geometric optimization.
  An example is shown below in simulation, we we improve a slowed-down gait's speed (<i>that more closely resembles how the robot walks in real-life</i>) by a factor of three.</p>
<br>

<!-- Video of robot walking faster with a more reasonable gait. -->
![Training Plot](/assets/images/projects/final/training.png)
<center><h2>Plot of training rewards over rollout number</h2></center>


![HSA Robot Moving in Pybullet](/assets/images/projects/final/hsa_slower_optgait.gif)
<center><h2>Optimized Pybullet gait, ~3x faster than initial policy</h2></center>

<p>Final results, aiming to demonstrate a complete sim-to-real gait pipeline, are still in production with the intention of preparing a conference submission! An absolute massive thank-you to my advisors Ryan Truby
  and Matt Elwin, along with Pranav Kaarthik, Francesco Sanchez from the Robotic Matter Lab. From Todd Murphey's Lab, Jake Ketchum, Muchen Sun, and Thomas Berrueta were all great resources and collaborators!
</p>

<br><br>


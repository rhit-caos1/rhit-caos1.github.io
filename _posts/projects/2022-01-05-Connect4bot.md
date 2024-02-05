---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "Python, AI, Mechatronics, Manipulation, Arduino"

project:
  title: "Connect 4 Master Robot"
  type: "Jekyll"
  url: "https://github.com/rhit-caos1/Connect4Bot"
  logo: "/assets/images/projects/Connect4Bot/cover_connect4.png"
  tech: "Python, AI (Alpha–beta Pruning), Mechatronics, Manipulation, Arduino"

images:
  - image:
    url: "/assets/images/projects/BotChoco/BotChocolate.gif"
    alt: "Making hot chocolate in X6 speed"
  - image:
    url: "/assets/images/projects/TrainControl/Flowchart.png"
    alt: "Flowchart"
  - image:
    url: "/assets/images/projects/BotChoco/Choco_CV2.jpg"
    alt: "Calibration"

youtubeId1: vKbEyXJEp4Y

---

{% include youtubePlayer.html id=page.youtubeId1 %}

### Intro
<br>


<p>This project, part of MECH_ENG 395: Industry 4.0 Manufacturing, introduces the Connect 4 Master Robot. Our innovation merges robotics and gaming, presenting a system capable of engaging in Connect 4 matches with human players. Beyond its gaming prowess, this robot boasts the potential to serve as a remote intermediary for players physically distant from each other, providing a live visual interface for an immersive, shared Connect 4 experience, transcending geographical boundaries.</p>
<br>

### Robot and control
<br>
<p>In this project, we employed a LewanSoul xArm as the physical computer player. This robot is operated using an Arduino board, which not only controls the robot but also detects the coins dropped by the human player onto the Connect 4 gaming board. To accomplish this, we utilized IR break sensors to accurately detect every coin drop through the top row of the borad.</p>

<br>

<p>During operation, the robot waits for the player to place the first coin. Using IR sensors, it detects the column where the coin is inserted, sending this data to the connected computer. The computer mirrors the game board and computes the optimal move. Once determined, the next action is relayed to the Arduino, which commands the robot to execute the move. The robot collects a coin from the feeder, drops it into the designated column on the playing board, and awaits the human player's next move. This sequence repeats until one side achieves victory. </p>

<br>

### Game Solver

<br>
<p>
In the realm of artificial intelligence and game theory, devising an effective Connect 4 solver necessitates strategic algorithms capable of exploring the vast decision space inherent to the game. One such approach that showcases remarkable efficiency is the implementation of the Alpha-Beta Pruning algorithm. Alpha-Beta Pruning is a sophisticated search algorithm used in adversarial games like Connect 4, where two players take turns making moves with conflicting objectives.</p>

<br>

The Alpha-Beta Pruning algorithm minimizes the number of nodes evaluated in the search tree, significantly reducing computational complexity. This is achieved by intelligently discarding branches of the search tree that are guaranteed to be irrelevant for the final decision. In the context of Connect 4, where the potential move possibilities escalate rapidly, Alpha-Beta Pruning proves invaluable in focusing the computational resources on the most promising paths, facilitating quicker and more effective decision-making.</p>

<br>

The solver leverages a heuristic evaluation function to assess the desirability of various game states, enabling the algorithm to make informed decisions about the optimal moves. By employing Alpha-Beta Pruning, the Connect 4 solver efficiently navigates the decision space, balancing computational resources and strategic decision-making to provide a robust and effective solution to this classic game.</p>
</p>
<br>

![AB_Pruning_example](/assets/images/projects/Connect4Bot/AB_pruning.png){:width="90%"}
<center><h5>An illustration of alpha–beta pruning. </h5></center>


### Github
<br>

<p>More information and source code can be found on the project's<a href="https://github.com/rhit-caos1/Connect4Robot" target="_blank"><u>GitHub repository</u></a>.<p>

<br>
<br>
<br>

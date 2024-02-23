---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "ROS, Python, CV, Manipulation, 3D Printing, Automation, CAD"

project:
  title: "Train Track Building Robot"
  type: "Jekyll"
  url: "https://github.com/rhit-caos1/trackbuilder_project/tree/Stage_1"
  logo: "/assets/images/projects/Final/Cover.jpg"
  tech: "ROS, Python, CV, Automation, 3D Printing,  CAD, Manipulation"

images:
  - image:
    url: "/assets/images/projects/TrainControl/Flowchart.png"
    alt: "Flowchart"


youtubeId1: RBCiYRlLWH0

youtubeId2: tdOf69g7VI0

youtubeId3: KCg4BJLEzvw

youtubeId4: Uzv7eY_zgps

# Set to true for publish !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
######################
######################
published: true
---

### Intro
<br>
<p>For my final project in the Northwestern MSR program, I focused on creating an autonomous system. This system enables a robot to independently identify, design, and assemble objects within its environment, responding to specific requirements without requiring human intervention.</p>

<br>

<!-- {% include youtubePlayer.html id=page.youtubeId1 %} -->
<h1>Full run video will not available until final paper is published. Some short timelapse videos below will show some components in the system and provide some simple concepts of the system.</h1>
<br>


<!-- ### Background
<br>
<p>As a former mechanical engineering student, my aspiration was to develop a comprehensive system capable of seamlessly integrating detection, design, manufacturing, and assembly processes. This vision drew inspiration from real-world scenarios, particularly the challenges faced in factory assembly lines where engineers often need to modify the setup to accommodate changes in products. Additionally, the concept of a train track laying machine, autonomously paving the way based on provided waypoints, played a pivotal role in shaping the specific task for this project. The final goal was to create a versatile system capable of adapting to dynamic environments, mirroring the flexibility required in both industrial settings and infrastructure development.</p>
<br>

![Idea](/assets/images/projects/Final/Concept.jpg){:width="90%"}
<center><h5>Two system above is heavily depends on human </h5></center> -->

### Project
<br>
<p>For this project, the goal was to test the concept of autonomous construction. The robot was tasked with building a complete toy train track circuit, utilizing track pieces randomly placed by humans in the working space. Through collaboration with Professor Michael Rubenstein, Matthew Elwin, and Ph.D. Shane Deng, we successfully developed the basic structure of the system. The robot executed the task precisely as expected, demonstrating the practical application of autonomous construction in a controlled environment.</p>
<br>

![Demo](/assets/images/projects/Final/Robot_Scan.gif){:width="90%"}
<center><h5>Robot is scanning workspace to detect existing tracks</h5></center>

<br>

<center><h5>After the detection, a piece of track is automatically generated to connect existing tracks and printed by 3D printer</h5></center>

<br>

![Demo](/assets/images/projects/Final/Part_Eject.gif){:width="90%"}
<center><h5>New part is ejected from the 3D printer</h5></center>

![Demo](/assets/images/projects/Final/Robot_Grasp_Place.gif){:width="90%"}
<center><h5>Robot is placing the new track to construct the track loop</h5></center>


![Demo](/assets/images/projects/Final/Cover.jpg){:width="90%"}
<center><h5>Robot placed several tracks successfully and is waiting for the new track to be printed</h5></center>

### Setup

## Hardware 

1. Franka Emika Panda Cobot
2. Intel realsense D435i
3. Creatliy CR40 Belt Printer
4. Raspberry Pi3 (connected to printer)

![Demo](/assets/images/projects/Final/Hardware_Setup.jpg){:width="90%"}
<center><h5>The working space and the hardware setup</h5></center>


## Software

1. ROS 2
2. Opencv
3. All packages mentioned in the <a href="https://github.com/rhit-caos1/trackbuilder_project/tree/Stage_1" target="_blank"><u>GitHub Readme</u></a> 

### System Design
<br>
<p>The software system comprises four major components: State Machine, Track Detector, Robot Controller, and Track Generator. The State Machine assumes a central role, orchestrating the entire system and processing tasks sequentially. The block diagram provided illustrates the interdependencies among these key components.</p>
<br>

![System](/assets/images/projects/Final/System_Diagram.jpg){:width="90%"}
<center><h5>System Design</h5></center>

<br>
<p>The State Machine is specifically engineered to command all system components and handle track-related information. The operational logic is elucidated in the following block diagram.</p>
<br>

![SateMachine](/assets/images/projects/Final/State_Machine_Simple.jpg){:width="90%"}
<center><h5>The simplified state machine pipeline</h5></center>

<br>
<p>The system waits for people to randomly place tracks in the workspace, starting its work once the placement is finished. It then follows the steps outlined in the State Machine to complete the track. In the following sections, we'll discuss each major part of the system in more detail.</p>
<br>

### Detection - Camera and Tag
<br>
<p>After the placement of tracks in the workspace by people is complete, it becomes improtant to update the robot on the current layout of the tracks. For this purpose, a detection system has been incorporated into the project. A key physical component of this system is the Intel RealSense D435i, affixed to the Franka robot's end effector, providing the necessary visual input for the robot to identify tracks in the workspace.</p>
<br>

![SateMachine](/assets/images/projects/Final/Realsense.jpg){:width="90%"}
<center><h5>Realsense D435i mounted on the end effector with extra lights</h5></center>

<br>
<p>Given the non-uniform shape of the tracks, conventional detection becomes challenging, especially in converting the shapes into positional information. To address this, a fiducial marker system is integrated. In contrast to utilizing existing tag families, a new tag system has been developed. This decision stems from the limitations encountered with other tags, particularly when 3D printed and attached to another part, leading to detection failures due to connectors on tag edges.</p>
<br>

![Tagtest](/assets/images/projects/Final/Tag_Experiment.jpg){:width="90%"}
<center><h5>The AprilTag system, known for its maturity in fiducial marking, demands a black border encircled by a continuous white boundary for optimal functionality. Any disruption, even a small connecting line to the border, can compromise detection accuracy.</h5></center>

<br>

![Tag_3d](/assets/images/projects/Final/Tag_3D.png){:width="50%"}
<center><h5>New tag design</h5></center>
<br>
<p>The custom-made tag design proves advantageous in detecting the orientation of the track, ensuring detection reliability even if parts of the tag outline are obstructed by connectors. The circular shape chosen for detection enhances robustness, allowing the detector to function effectively even if the circle is incomplete. Once the center of the circles is identified, a PnP (Perspective-n-Point) solver is employed to translate this information from the camera frame into real-world orientation.</p>
<br>

![Tag_detect](/assets/images/projects/Final/Tag_detection.png){:width="70%"}
{% include youtubePlayer.html id=page.youtubeId4 %}
<center><h5>Detecting the Tag position and orientation</h5></center>
<br>

<p>The robot system detects all tags within the scanning space, relaying tag position information to the robot controller and state machine. The state machine then updates track information and signals the generator to create the next track.</p>
<br>



<!-- Video: Scan workspace
<br> -->

<h1>Right Now a new detector is under testing which could allow us remove the tag from the track</h1>

<br>

### Design - CAD Generator
<br>
<p>The track design is based on the Brio toy train track. The system generated intermediate tracks based on the provided start and end track information after scan information updated. After detection, the system reorganizes the tracks into a specific order, forming a closed loop. This track information is then relayed to the generator, updating it each time the detector detect the change in the environment. The Bezier curve generator plays a pivotal role in creating new curves that connect to the given track.</p>
<br>

![Curve_Gen](/assets/images/projects/Final/Curve_gen.png){:width="100%"}
<center><h5>Create Bezier Curve according to the given start and end point information</h5></center>
<br>
<p>The system closely monitors the minimum curvature of the generated curve, ensuring that the new track accommodates the original Brio train's passage. Subsequently, the curve is automatically transmitted to a track generator, which generates the track based on the curve's shape. Tags and specially designed connectors are concurrently added to the track. The following image showcases the generated track in the OpenSCAD model.</p>
<br>

![Track_Gen](/assets/images/projects/Final/Track_Gen.png){:width="100%"}
<center><h5>Generate the track cad with tag connected by using Bezier Curve as the reference</h5></center>
<br>
<p>OpenSCAD facilitates the conversion of this model into an STL file for processing by the slicer. The slicer, in turn, transforms the design into G-code, suitable for the 3D printer.</p>

<br>

<p>(Considerable effort has been invested in this phase to optimize both the tag and track designs, ensuring ease of detection and 3D printing compatibility)</p>
<br>

![Track_Evolution](/assets/images/projects/Final/Evolution.jpg){:width="100%"}
<center><h5>Versions of tags and tracks we developed and tested.</h5></center>
<br>



### Manufacture - Slicer and Printer:

<br>
<p>The slicing process is carried out using Kiri-Moto, offering a command-line interface for seamless integration. Once the STL file is generated, the system converts it to a customized G-code, tailored to meet our specific printing requirements.</p>
<br>

![Slicer](/assets/images/projects/Final/Kiri_Slicer.png){:width="50%"}
<center><h5>Very useful slicer and works well in command line</h5></center>
<br>
<p>The implementation of OctoPrint on a Raspberry Pi, connected to the Creality CR30 printer, streamlines the printing process. Once the G-code is prepared, the control computer transmits the file to the printer, while the Raspberry Pi monitors the print progress and provides real-time status updates.</p>
<br>

![Printer](/assets/images/projects/Final/Printer.jpg){:width="80%"}
<center><h5>Belt printer is printing new track for the robot system</h5></center>
<br>
<p>Given the unique design of the printer as a belt printer, parts are effortlessly ejected from the print bed by simply rolling the belt forward. The newly printed track piece neatly falls into a designated area within the workspace, ready for the robot to collect upon completion of the printing process.</p>
<br>
<!-- {% include youtubePlayer.html id=page.youtubeId2 %} -->
![Printer](/assets/images/projects/Final/Part_Eject.gif){:width="80%"}
<center><h5>Belt printer is ejecting finished train track (time x9)</h5></center>
<br>

### Manipulation – Robot

<p>The Franka Emika Panda Cobot arm plays a crucial role in this project. With the camera positioned at the end effector, the robot not only handles the movement of track pieces but also serves as an essential component of the detection pipeline. Additionally, the robot is programmed with specialized movements to enhance detection accuracy and address misalignment issues effectively.</p>

<br>

![Robo_Scan](/assets/images/projects/Final/Robot_Scan.gif){:width="70%"}
<center><h5>Robot is scanning tracks after system started</h5></center>
<br>

![Robo_Place_Track](/assets/images/projects/Final/Robot_Grasp_Place.gif){:width="70%"}
<center><h5>Robot is placing the new track to construct the track loop</h5></center>
<br>

<br>

### Future Improvements
<br>
<p>Detection Accuracy: Presently, the detection accuracy hovers around 1-2mm. Our goal is to elevate this precision, aiming for a level of accuracy comparable to what April tags can achieve.</p>
<br>
<p>Design: While SCAD has been instrumental in our design process, unexpected assertion errors have surfaced during file conversion to STL via the command line. Considering this, we are exploring more stable alternatives for design work in the future.</p>
<br>
<p>Manufacture: The current printing time is notably lengthy. Future enhancements could involve optimizing printer performance to boost printing speed or upgrading to a more efficient printer.</p>
<br>
<p>Manipulation: The Franka robot experiences intermittent malfunctions, likely due to bugs within the system. Addressing this issue requires revising content in the Franka ROS2 repository to ensure the robot's stability and reliability in operation. This is crucial for the success of the overall project.</p>

<br>
### Github
<br>
<p>More information and source code can be found on the project's<a href="https://github.com/rhit-caos1/trackbuilder_project/tree/Stage_1" target="_blank"><u>GitHub repository</u></a>.<p>

<br>
<p>(Paper in progress, all code will release to public after paper published)<p>

<br>
---
title: Navigator
description: A Step Towards Autonomous Agile Flight Mastery
author: ahmed
date: 2024-09-30 12:00:00 +0800
categories: [Projects, Aerial Robotics]
tags: [Final Year Design Project]
pin: true
math: true
mermaid: true
image:
  path: /assets/img/navigator/navigator.jpg
  lqip: /assets/lqip/navigator/navigator.jpg
  alt: 
---

## Introduction

Navigator is the quadcopter of my final year design project. A solo venture lying at the intersection of modern control theory, flight dynamics modelling, aerial robotics, RC hobby, computer aided design, and design for additive manufacturing. It was a self-crafted research avenue that allowed me to fully experience controller development for aerial vehicles from scratch. It was a challenging and stimulating experience that required a good engineering knowledge from multiple disciplines. This was the first step, taken by me, at my university campus to build towards autonomous agile vision-based quadcopter flight. The idea was to leave behind a solid platform and methodology to be adopted by future researchers to achieve this sophisticated aerial prowess.

### Salient Features and Scope

<ul>
  <li>Developing a deep understanding of control design philosophy</li>
  <li>Proposing a well researched methodology enabling agile quadcopter flight</li>
  <li>Flight Dynamics Modelling of a quadcopter plant for Model Based Design</li>
  <li>Deriving a Model Predictive Controller (MPC) analytically and linearizing it through Linear Parameter Varying (LPV) approach</li>
  <li>Assembling a global control architecture of cascaded Feedback Linearization and MPC controllers</li>
  <li>Successful demonstration of 3D trajectory tracking in simulation</li>
  <li>Fabrication of a GPS enabled high speed quadcopter</li>
  <li>CAD modelling and Fused Deposition Modelling of customized parts</li>
  <li>Generation and implementation of a hardware ready flight code on a Jetson Nano</li>
</ul> 

### Why This Project?

The world is moving towards an aerial driven future as it is becoming more and more customary to see the airspace being unlocked for commercial purposes. It is expected, by 2030, that the <a href="https://www.grandviewresearch.com/industry-analysis/global-commercial-drones-market" target="_blank">commercial drone market in the United States</a> will reach roughly 57 billion USD. Applications ranging from agricultural, exploration, search and rescue, logistics, cinematography, and defence are only to name a few. To maximise the potential of this aerial future requires a solid understanding of the foundational concepts associated with these technologies and hands on training with their state-of-the-art methodologies.

May these airborne machines be rotary, fixed-wing, or hybrid in nature, the big ideas encompassing them remain unchanged. The great thing about quadrotors in particular is the ease of accessibility in terms of hardware, open-source software, available coursework, scientific literature, and a like-minded community. Therefore, this project was crafted around quadcopters to get a solid feel for the challenges and strategies involved to solve problems pertaining to aerial robotics.

### Control Challenges for Aerial Autonomy

The control problem of any aerial application lies at the heart of vehicle dynamics and navigation. Typically, a navigation problem can be broken down into sub-problems of sensing, planning, and control. So, in essence, things like what are the mechanics of the air vehicle we are trying to control? How do we setup the sensors? How do we utilize sensor data to construct a reliable estimate of our position and attitude in space? How does the vehicle decide what its flight plan should be and how do we set it up in a manner that allows for an efficient way of replanning if the need arises? Once we have a flight path, how do we go about stabilizing our vehicle and executing the set path whilst meeting our requirements? What does the simulation environment look like? Once confident about our design, how do we go about implementing them in reality? What limitations do we foresee regarding our practical implementation and how do we plan in advance to mitigate them? These all are some of the most basic challenges that needed to be overcome. As evident there is a great deal of autonomy and intelligence required to enable reliable future aerial operations.

---

## Control Philosophy and Proposed Methodology

The project began with the formulation of a novel and adaptable methodology, serving as the foundation for the design process. As an essential first step, extensive research was conducted to thoroughly understand the prevailing practices in controller design. This groundwork culminated in the development of a comprehensive framework for the controller design process, addressing the complexities inherent in achieving high-agility and speed in maneuvering quadcopters. These complexities stem from the non-convex nature of objective functions, reliance on noisy parameter evaluations during tuning, and the need for dynamically adjusting parameters across different trajectory segments.

The resulting framework consolidates over 15 years of research, spanning early demonstrations of vision-based autonomous flight to recent milestones achieved in human vs algorithmic piloting abilities. It highlights key challenges such as perception-to-action dependence, domain shifts, and sensor limitations, offering innovative solutions like hybrid simulation-real-world approaches. Additionally, the framework evaluates potential drone platforms suited for hardware implementation, and that are geared towards research and development. This work was presented as a conference paper at the Smart Mobility and Logistics Ecosystems conference at KFUPM, published through a peer-reviewed process. For a graphical overview of the design philosophy refer to the image below. For a detailed treatment of the subject, you can read my conference paper using this <a href="https://doi.org/10.1016/j.trpro.2025.03.100" target="_blank">link</a>.

![Philosophy Flowchart](/assets/img/navigator/control-design-philosophy.jpg){: lqip="/assets/lqip/navigator/control-design-philosophy.jpg"}
_Illustration of a general-purpose control design philosophy_

---

## Vehicle Dynamics Modelling

There were two reasons to model my quadcopter’s dynamics. Firstly, to derive a plant model needed to test and tune the controller in simulation. Secondly, for the modelling of the controller itself. The need for the latter arises from the nature of the project goals.

As explained in my paper, <a href="https://github.com/uzh-rpg/agilicious" target="_blank">Agilicious by ETH Zurich</a> was the platform chosen for the hardware implementation part of the project. Geared towards agile quadrotor research and harbouring substantial amount of work under its belt made it the go-to choice. To understand the control architecture of the platform better there was a need to work towards modern control theory concepts, Model Predictive Control in particular.

To develop a sound understanding of the vehicle dynamics modelling and modern control system design, I followed these two courses by Mark Misin: <a href="https://www.udemy.com/course/applied-systems-control-for-engineers-modelling-pid-mpc/" target="_blank">Applied Control Systems 1</a> and <a href="https://www.udemy.com/course/applied-control-systems-for-engineers-2-uav-drone-control/" target="_blank">Applied Control Systems 3</a>. Both courses are very elaborate, clear and enabling in terms of their content.

For vehicle dynamics modelling a solid understanding of the following concepts has been developed:
<ul>
  <li>Underactuated systems and associated limitations</li>
  <li>Setting up of system control inputs for a quadcopter</li>
  <li>Euler’s rotation theorem and its unique conventions</li>
  <li>Rigorous mathematical and graphical investigation of relationship between Extrinsic and Intrinsic rotational conventions</li>
  <li>Benefits of using the intrinsic approach for particular control problems</li>
  <li>Derivation of the Newton Euler formulation for a 6-DOF rigid body system</li>
  <li>Mathematical modelling of gravity, control inputs, and gyroscopic precession</li>
  <li>Representing the obtained quadcopter specific equations of motion in the state space formulation</li>
  <li>Formulation of a motor mixing algorithm with the help of the Blade Element Momentum theory</li>
</ul> 

If any of the topic interests you, then feel free to take a look at my course notes by clicking the image below. The notes especially go in great detail to investigate rotational matrices with hand done derivations; these are very important for any robotics project due to variety of frame systems that are simultaneously in play. Also, at the end of the notes you will find a list of all the assumptions taken and room for improvement that you may work on to make the plant model more accurate.

![FDM Notes Preview](/assets/img/navigator/navigator-FDM-notes-preview.png){: lqip="/assets/img/navigator/navigator-FDM-notes-preview.jpg"}
_<a href="{{site.url}}/assets/docs/navigator/navigator-FDM-notes.pdf" target="_blank">Click to download the PDF for my FDM notes</a>_

---

## Control Architecture Design

This part of the project deals with a very important question. Given a flight path, how does a drone go about executing it? Following the coursework of Mark Misin, a control architecture of a feedback linearization outer-loop and a model predictive inner-loop controller (MPC) has been employed.

![Control Architecture](/assets/img/navigator/controller-architecture.png){: lqip="/assets/img/navigator/controller-architecture.jpg"}
_Control Architecture_

The feedback linearization, also known as “exact linearization”, is a non-linear control technique that transforms a non-linear system into a fully or partially decoupled linear one, without loss of any accuracy, so that linear control strategies may be used. Within this architecture this outer loop controller works as a position controller that computes the quadcopter orientation that is needed to get to the reference position provided by the planner.

The inner-loop model predictive control receives the target attitude angles to produce the most optimum control commands for the scenario. It does this by planning in advance for a specified number of timesteps known as the horizon period. A set of optimization objectives are defined which are then used to minimize a mathematical cost function, over this finite horizon period, to determine the best system input. This is done in a receding horizon fashion. The inner-loop runs at a higher frequency to try and catch the reference set by the outer-loop. For this we say that the inner-loop has dynamics stronger than the outer-loop.

The MPC controller needs equations of motion to make such predictions. If the attitude equations are visited in my course notes, then it is found that there are non-linearities present in them. To apply the formulations of a linear MPC controller to our non-linear set of equations, a two-fold process is used. First, the transfer matrix is simplified to simplify the EOMs from rates to Euler angles themselves. Secondly, linear parameter varying (LPV) is applied to put the EOMs into a linear format. The continuous set of equations are then discretised. Finally, a cost function is formulated, simplified, and solved for set goals.

All of these steps are mathematically intensive and thus, I am including my course notes in this section for anyone who may be interested in reading further. It is a good read for anyone new to optimal and quadrotor control and the notes provide reasoning for all design choices made.

![Controller Design Notes Preview](/assets/img/navigator/navigator-controller-design-notes-preview.png){: lqip="/assets/img/navigator/navigator-controller-design-note.jpg"}
_<a href="{{site.url}}/assets/docs/navigator/navigator-controller-design-notes.pdf" target="_blank">Click to download the PDF for my controller design notes</a>_

---

## Towards Hardware Implementation

Once designed there is a need to evaluate the performance and assess the potential of the controller. Testing directly at a hardware level is a risky task as any unforeseen design flaw can lead to a hazard of damaging equipment, life, and surroundings. To avoid this, there is a very important step in control design process to perform Software in the Loop Simulations (SILS). Simulations are an excellent way to perform trade-studies, highlighting limitations, monitoring improvements, and enhancing realism of plant model and controller design by emulating flight conditions, scenarios, and disturbances that otherwise may not be possible to be replicated physically in a cost effective and reliable manner. After the design undergoes significant changes in this phase and a considerable confidence of the design is developed, the next step is to work towards its hardware implementation.

Developing a completely new controller and implementing it physically is an immensely challenging task; due to time constraints this isn’t within the scope of this project. It has been previously mentioned that the hardware platform chosen for this project is ETH Zurich’s Agilicious framework. Furthermore, the purpose of the analytically designed controller was to get a direct hand on with the important concepts that go into making one and better understand the adopted framework. Nonetheless, it would be exciting to see the engineered mathematics in action. For this I used the companion Python script provided by Mark Misin in his course and tweaked it to test a manoeuvring flight scenario.

![Python Trajectory Tracking](/assets/img/navigator/controller-python-simulation.gif){: lqip="/assets/lqip/navigator/controller-python-simulation.jpg"}
_Model Predictive Control in action_

The hardware phase of the project is a major one. It’s an assimilation of a lot of skills including but not limited to Ubuntu Operating System, Robot Operating System, Docker, CAD Modelling, Design for Additive Manufacturing, Additive Manufacturing, Betaflight Firmware, and Jetson Nano. Through continuous troubleshooting a very strong understanding for the involved frameworks was developed. This phase although involved development of software and hardware in parallel, for the purposes of this blog I will be presenting first the hardware fabrication portion, followed by a software development portion, and then finally an integration and testing portion.

![Navigator](/assets/img/navigator/navigator-cyberpunk.gif){: lqip="/assets/lqip/navigator/navigator-cyberpunk.jpg"}
_Navigator powered on_

---

## Hardware Fabrication

Ideally, the fabricated platform should match that of Agilicious’ to minimize the need of manually tweaking the controller parameters to work with the quadrotor. Below is a list of all the major components used:

| Component Used                            | Agilicious Reference                                             | Description          | Notes                                                                                                                            |
| ----------------------------------------- | ---------------------------------------------------------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Jetson Nano                               | Jetson TX2                                                       | Main Compute Unit    | A cheap alternative to perform non-vision based agile flight                                                                     |
| Reference Carrier Board                   | ConnectTech Quasar                                               | Breakout Board       | The reference board comes with the Jetson Nano Developer Kit                                                                     |
| Unbranded F722 Flight Controller          | TMotor F7 Flight Controller                                      | Low-Level Controller |                                                                                                                                  |
| 60A 3-6S BLHeli-S                         | F55A Pro II 3-6S 4-in-1 ESC                                      | ESC                  | Ordered alongside the FC as a stack. BLHeli_S natively doesn’t support bi-directional DShot, which could be a matter of concern. |
| Mark4 HD6 Carbon Fiber                    | Armattan Chameleon 6"                                            | Main Plate           |                                                                                                                                  |
| TMotor Veloc V2306 V2.0                   | TMotor Veloc V2306 V2.0                                          | Motors               |                                                                                                                                  |
| Dalprop T5148 Propellers                  | Azure Power SFP 5148                                             | Propeller            |                                                                                                                                  |
| CNHL 1300mAh 100C                         | Tattu R-Line 4s 1800mAh 120C                                     | Battery              |                                                                                                                                  |
| 2A 4.5-40V to 5V Step-down Buck Converter | Recom Power R-78B9.0-2.0                                         | Voltage Converter    |                                                                                                                                  |
| Beitian BN-880 GPS                        | Expensive Motion Capture Systems / Intel RealSense Depth Cameras | Localisation         |                                                                                                                                  |

It is clear from the comparative list that my quadcopter isn’t an exact replica of Agilicious. There are several reasons for this. First, was no market availability of the following items: Armattan Chameleon 6”, Azure Power SFP 5148, and Tattu R-Line 4s 1800mah 120C. For these the closest match in market was sought and bought. Second, due to budget constraints I went for an economical build. A branded F722 flight controller stack was avoided, but most importantly due to an absence of a need of camera vision implementation, a Jetson Nano was used rather than the more powerful Jetson TX2 compute unit. Third, there was an intent of an outdoor flight because of which a Beitian BN-880 GPS unit was used instead of expensive motion capture systems for localisation. The use of a GPS with Agilicious and compiling the Agilicious flight code on a Jetson Nano both hadn’t been performed before and thus added novelty to the project.

Deviations caused due to these reasons necessitated fabrication of custom parts. To do this, I used Autodesk Inventor. A good design is foundational for good performance for which all parts were designed with clear-cut objectives in mind. Out of all parts, the most intricate one to make was the top plate. The top plate had to accommodate majority of the components, have a minimal footprint to prevent airflow obstruction to the propellers, maintain alignment with other parts, and possess adequate structural strength in critical load regions. Keeping the high-speed specs of the build and agile fight in mind, it was imperative that all of the designed parts were sleek and allowed for meticulous and seamless wiring. With Model Predictive Control concepts in mind, I knew I had to keep the CG as close to the geometric centre as possible. Lastly, all designs had to be additive manufacturing friendly.

All goals were successfully met! Due to the reproducible and empowering intent of the project, all CAD designs, alongside the complete quadcopter 3D model can be found on <a href="https://grabcad.com/library/navigator-3" target="_blank">GrabCAD</a>. The final weight of quadcopter came out to be 806g.

![Wire Management](/assets/img/navigator/navigator-wire-management.jpg){: lqip="/assets/img/navigator/navigator-wire-management.jpg"}
_Snug and well thought out wiring scheme for high speed flights_

Just like the top plate, the GPS mount and Jetson protection cage designed for the project had salient features. The GPS mount required a clear view of the sky while ensuring minimal vibrations and drag at high speeds. The protection cage was designed to be breakable and modular in fashion. Breakable for high resilience and modular for easier replacements and easy access to the underlying Jetson Nano. The design provided excellent performance in protecting the processing unit during test flights.

In case you are looking for an extended list of components that I used in the project, refer to the additional items below for ease of build.

| Item                                      | Quantity | Description                                                                                                                    |
| ----------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| LINCUKOO/Realtek: Mini Wifi Dongle 8811CU | 1        | Wifi receiver for Jetson Nano                                                                                                  |
| Velcro Strap 300mm                        | 2        | To tie battery on the top plate                                                                                                |
| Silicon Wire 20AWG                        | \-       |                                                                                                                                |
| Heat Shrink Tube 6mm                      | \-       |                                                                                                                                |
| Heat Shrink Tube 3mm                      | \-       |                                                                                                                                |
| Parallel Adapter XT60                     | 1        | Dividing the battery power into parallel streams. One for the low-level controller stack and the other one for the Jetson Nano |
| XT60 Battery Male Plug                    | 1        |                                                                                                                                |
| Rubber Standoffs                          | \-       | To elevate the top plate over the Mark4 frame                                                                                  |
| Screws, Nuts & Bolts                      | \-       | Varying sizes for different components. Use plastic or acrylic bolts for the breakable protection cage base pieces             |

---

## Software Stack & Flight Code

Much of the heavy lifting in this project lay not in hardware integration, but in the layered, intricate setup of the software stack that powered the quadcopter’s autonomy. While Agilicious provides a robust simulation and real-flight control framework, its deployment on non-standard embedded platforms like the Jetson Nano is far from plug-and-play.

From a solo-engineering perspective, this part of the project demanded a steep learning curve. I had to go beyond the typical application layer and work across low-level driver configuration, containerized build environments, real-time data protocols, and systems debugging — all while navigating incomplete documentation and untested hardware combinations.

What follows is a breakdown of the software challenges I encountered and the solutions I implemented — with a focus on learnings and the technical depth gained along the way.

### Core Tools & Frameworks

| **Category**           | **Tools / Frameworks**                                               |
|------------------------|----------------------------------------------------------------------|
| OS & Environment        | Ubuntu 20.04, Bash, Systemd, DKMS                                    |
| Containerization        | Docker, NVIDIA-Docker 2, Dockerfiles, Container Volumes              |
| Flight Stack            | Agilicious (UZH), Betaflight CLI                                     |
| Robotics Middleware     | ROS Melodic, Catkin, ROS Topics, roslaunch                           |
| Protocol Bridges        | MAVROS (MAVLink–ROS bridge), SBUS                                    |
| Debugging Utilities     | screen, fuser, dmesg, modprobe, rqt_graph                            |

### Ubuntu Installation and System Setup

The software journey began with installing Ubuntu on my laptop — a process that, despite appearing straightforward, proved otherwise. The system bypassed the Ubuntu Live USB entirely and booted straight into Windows. Once installation began, the 'Install Ubuntu' option failed to appear, and later attempts were blocked by `grub-probe` errors and `/cow` path conflicts. Even after successful installation, persistent ACPI errors, GRUB bootloader failures, and kernel-driver mismatches continued to hinder progress.

Resolving these required significant hands-on debugging. I had to manually dissect online forum threads, compare kernel logs, reconfigure boot parameters, and switch kernel versions to regain Wi-Fi functionality without compromising dependencies. Along the way, I learned to adjust environment variables like `PATH` to resolve issues and became fluent in kernel module handling via tools like `dkms` and `modprobe`.

### Dockerizing Agilicious on Laptop and Jetson Nano

With the operating system stabilized, the next major step was setting up the Agilicious code base, which is recommended to be run using Docker. On my x86 laptop, the image built without modification, but understanding how Docker worked, managing `nvidia-docker-2`, and configuring the ROS-enabled container environment required focused effort. While working through this phase, I also encountered a small typo in the official Agilicious documentation — a detail that could easily cause confusion for those new to these frameworks.

Transitioning to Jetson Nano introduced a new set of challenges: the original Dockerfile failed due to architecture mismatches, unsupported binaries, and pip-based dependency errors. I began by learning the core concepts of Docker — how images are structured, how containers run in isolation, and how to work with layered builds. After verifying the setup on my laptop, I modified the Dockerfile for Jetson Nano to resolve architecture-specific issues. This included replacing amd64-specific binaries, patching package installations (such as `scipy`), and adjusting dependencies that broke during build.

### Establishing ROS Communication Between Jetson and Laptop

With the Agilicious codebase built and running on the Jetson Nano, I configured a multi-machine ROS setup with my laptop acting as the ROS master. This allowed high-level commands to be issued from the laptop while the Jetson handled onboard execution. The distributed configuration was successfully brought online; when sending an arming command from the master’s RViz interface, the Jetson-side terminal acknowledged the input — confirming that the message had been received and interpreted at the ROS level. However, the drone itself failed to arm, indicating an unresolved issue in the communication link between the Jetson and the flight controller.

Similarly, telemetry data such as battery voltage or sensor feedback was not visible in RViz on the laptop — not due to faulty ROS networking, but likely because the Jetson was not successfully receiving data back to the Flight Controller. In short, the inter-device ROS pipeline was functioning, but the connection between Jetson and the hardware layer remained to be resolved.

![Software Stack](/assets/img/navigator/software-stack.png){:lqip="/assets/lqip/navigator/software-stack.jpg"}

### Unlocking Dual UART Support on Jetson Nano

One of the most technically involved challenges in the project was configuring two separate UARTs on the Jetson Nano — a requirement that only became clear after extensive debugging. The wiring diagram in Agilicious’ documentation showed connections for the Jetson TX2 via the ConnectTech Quasar carrier board, using a single UART interface. This was misleading: even for TX2 setups, successful MAVLink and SBUS communication required two separate UARTs. Following that diagram led to the incorrect assumption that a single UART could support both protocols.

Upon deeper investigation, including reading through NVIDIA developer threads and product design guides, I discovered that the Jetson Nano has three UARTs: one exposed on the 40-pin GPIO header (`ttyTHS1`), another on the M.2 slot (`ttyTHS2`), and a third serial debug port (`ttyS0`). Crucially, `ttyS0` is the only other accessible UART besides `ttyTHS1`, and it is, by default, locked by the system for serial console access.

Identifying `ttyS0` as the second usable UART was a key breakthrough. The port showed sluggish or incorrect behavior during loopback tests, and further inspection with `fuser` and `ps` revealed that the `agetty` service was occupying the port. To disable it reliably across reboots, I used systemd's `mask` mechanism — effectively freeing the UART for general-purpose use. This enabled bidirectional communication with the Flight Controller, resolving both arming and telemetry issues observed earlier.

### Adapting Agilicious Source Code for Custom GPS Integration

Once the basic communication and launch structure was stable, I focused on adapting the software pipeline to support my outdoor GPS-based flight configuration. Agilicious by default supports motion capture or depth camera pipelines; GPS was not part of its native implementation. To integrate GPS data into the estimation pipeline, I studied the internal source code structure of Agilicious, explored the launch files, and analyzed ROS topic flows using `rqt_graph` and `rostopic echo`.

At this point, I figured that essential ROS packages like MAVROS — Agilicious' bridge to the MAVLink protocol — were not installed by default. This was critical, as MAVROS is responsible for interpreting and exposing telemetry data such as battery voltage, IMU readings, and GPS coordinates from the flight controller to the ROS ecosystem. Installing it, however, wasn’t straightforward. A key dependency, GeographicLib, failed to download due to a server issue. To resolve this, I manually retrieved the necessary dataset files from SourceForge and placed them in the appropriate path within the ROS environment inside my Docker container — a task that sharpened my fluency with container file systems and ROS package structures.

I eventually wrote a custom GPS node that subscribed to `/mavros/global_position/local` and `/mavros/imu/data` and published the required message formats to `/agiros_pilot/odometry_estimate` and `/agiros_pilot/pose_estimate`. To support this, I modified the `CMakeLists.txt` of the agiros package, added the new node to its source tree, and edited the relevant launch files to register and launch the node. The result was a working data bridge between MAVROS and the Agilicious controller. Writing this node not only ensured system-level cohesion but also deepened my understanding of ROS message composition and inter-node communication.

### Skills Acquired & Tools Mastered

The steps outlined here cover the major components required to get the flight code installed and operational on Jetson Nano. This includes adapting the Docker environment, enabling and configuring UART communication, creating ROS nodes for GPS integration, and navigating the Agilicious codebase.

While these were key milestones, they are not an exhaustive account. Other steps — like flashing the Jetson Nano, configuring shell environments, resolving ROS dependency issues, and handling version mismatches — also played important roles. These processes contributed to a well-rounded set of skills in system configuration and integration, containerized development, and debugging.

Given the undocumented challenges and Jetson-specific edge cases involved, I may write a follow-up post that offers a detailed, step-by-step troubleshooting guide and practical tips for setting up this software stack on a Jetson Nano.

| **Domain**             | **Skills Developed**                                                                 |
|------------------------|--------------------------------------------------------------------------------------|
| System Configuration   | Kernel module handling, environment variable setup, multi-kernel troubleshooting     |
| Containerization       | Docker image authoring, modifying Dockerfiles, NVIDIA-Docker installation            |
| ROS Development        | Writing custom nodes, editing CMakeLists, ROS topic/rqt_graph/rosbag usage           |
| Firmware & Serial I/O  | Betaflight CLI use, UART testing, agetty service masking, FC–Jetson interfacing      |
| Debugging              | Log analysis, ROS message tracing, dependency resolution through forum research      |
| Integration            | Coordinating Jetson–laptop ROS systems, bridging MAVROS with Agilicious pipeline     |

---

## Flight Integration & Limitations

With the software stack operational across Jetson Nano and my laptop, I moved to full system integration. Bench tests without propellers were conducted to assess controller response to a 1.5-meter hover command. Outdoors, altitude estimates fused from **GPS + barometer** by the firmware yielded stable results. Indoors, however, reliance on barometric data alone led to erratic readings; highly sensitive to wind wash, rendering hover control unreliable. To improve indoor estimation, I explored the possiblity of fusing barometer and IMU data. But Betaflight’s MAVLink stream lacked IMU output; source code inspection confirmed angular rates were hardcoded and linear accelerations missing. Without IMU access, meaningful fusion was blocked at the firmware level. Also, modification of Betaflight firmware wasn't in the scope of the project and thus this avenue wasn't explored further.

An outdoor flight attempt followed. Arming via RViz showed no immediate response, but moments later Navigator unexpectedly took off — a misconfigured launch file had triggered the Agilicious backup pipeline. Navigator hovered stably for a few seconds, then slightly banked and slowly descended into a soft crash. No video or logs were captured due to the unanticipated take-off.

Repairs and correcting the pipeline took the next day, but worsening weather forced me indoors for further testing. To ensure safety, I moored the drone. As anticipated from prior bench behavior, indoor flight was unstable. Without GPS, altitude estimation failed under barometric noise. A sneak peek into the flight test can be analyzed alongside barometric reading and collective thrust commands.

{%
  include embed/video.html
  src='/assets/vid/indoor-flight.mp4'
  poster='/assets/lqip/navigator/'
  title='Navigator indoor flight testing'
  autoplay=true
  loop=true
  muted=false
%}

The impact with the ceiling was strong which led to overheating of the Flight Controller in post flight equipment check. This was heartbreaking as I no longer had luxury of time to get hands on a new one and solder it onto Navigator before the project deadline. This flight, although seemingly short and abrupt, was a demonstration of reliable operation of telemetry links, ROS communications, and controller logic. I am positive that the degree of integration that I have performed for the project can deliver point to point autonomous outdoor navigation in GPS enabled environment. Betaflight firmwware modification was also highlighted as a major lead for future work enabling accurate state estimation.

---

## But Seriously, Why This Project?

Because I think aerial robotics is awesome, control theory is fascinating, and because this project earned me the best final year project award :)

![Convocation '24](/assets/img/navigator/best-fydp.png){: lqip="/assets/lqip/navigator/best-fydp.jpg"}

---
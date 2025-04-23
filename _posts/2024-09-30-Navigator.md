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
  lqip: 
  alt: 
---

## Introduction

Navigator is the quadcopter of my final year design project. A solo venture lying at the intersection of modern control theory, flight dynamics modelling, aerial robotics, RC hobby, computer aided design, and design for additive manufacturing. It was a self-crafted research avenue that allowed me to fully experience controller development for aerial vehicles from scratch. It was a challenging and stimulating experience that required a good engineering knowledge from multiple disciplines. This was the first step, taken by me, at my university campus to build towards autonomous agile vision-based quadcopter flight. The idea was to leave behind a solid platform and methodology to be adopted by future researchers to achieve this sophisticated aerial prowess.

### Why This Project?

The world is moving towards an aerial driven future as it is becoming more and more customary to see the airspace being unlocked for commercial purposes. It is expected, by 2030, that the <a href="https://www.grandviewresearch.com/industry-analysis/global-commercial-drones-market" target="_blank">commercial drone market in the United States</a> will reach roughly 57 billion USD. Applications ranging from agricultural, exploration, search and rescue, logistics, cinematography, and defence are only to name a few. To maximise the potential of this aerial future requires a solid understanding of the foundational concepts associated with these technologies and hands on training with their state-of-the-art methodologies.

May these airborne machines be rotary, fixed-wing, or hybrid in nature, the big ideas encompassing them remain unchanged. The great thing about quadrotors in particular is the ease of accessibility in terms of hardware, open-source software, available coursework, scientific literature, and a like-minded community. Therefore, this project was crafted around quadcopters to get a solid feel for the challenges and strategies involved to solve problems pertaining to aerial robotics.

### Control Challenges for Aerial Autonomy

The control problem of any aerial application lies at the heart of vehicle dynamics and navigation. Typically, a navigation problem can be broken down into sub-problems of sensing, planning, and control. So, in essence, things like what are the mechanics of the air vehicle we are trying to control? How do we setup the sensors? How do we utilize sensor data to construct a reliable estimate of our position and attitude in space? How does the vehicle decide what its flight plan should be and how do we set it up in a manner that allows for an efficient way of replanning if the need arises? Once we have a flight path, how do we go about stabilizing our vehicle and executing the set path whilst meeting our requirements? What does the simulation environment look like? Once confident about our design, how do we go about implementing them in reality? What limitations do we foresee regarding our practical implementation and how do we plan in advance to mitigate them? These all are some of the most basic challenges that needed to be overcome. As evident there is a great deal of autonomy and intelligence required to enable reliable future aerial operations.

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

---

## Control Philosophy and Proposed Methodology

The project began with the formulation of a novel and adaptable methodology, serving as the foundation for the design process. As an essential first step, extensive research was conducted to thoroughly understand the prevailing practices in controller design. This groundwork culminated in the development of a comprehensive framework for the controller design process, addressing the complexities inherent in achieving high-agility and speed in maneuvering quadcopters. These complexities stem from the non-convex nature of objective functions, reliance on noisy parameter evaluations during tuning, and the need for dynamically adjusting parameters across different trajectory segments.

The resulting framework consolidates over 15 years of research, spanning early demonstrations of vision-based autonomous flight to recent milestones achieved in human vs algorithmic piloting abilities. It highlights key challenges such as perception-to-action dependence, domain shifts, and sensor limitations, offering innovative solutions like hybrid simulation-real-world approaches. Additionally, the framework evaluates potential drone platforms suited for hardware implementation, and that are geared towards research and development. This work was presented as a conference paper at the Smart Mobility and Logistics Ecosystems conference at KFUPM, published through a peer-reviewed process. For a graphical overview of the design philosophy refer to the image below. For a detailed treatment of the subject, you can read my conference paper using this <a href="https://doi.org/10.1016/j.trpro.2025.03.100" target="_blank">link</a>.

![Philosophy Flowchart](/assets/img/navigator/control-design-philosophy.jpg)
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

![FDM Notes Preview](/assets/img/navigator/navigator-FDM-notes-preview.png)
_<a href="{{site.url}}/assets/docs/navigator/navigator-FDM-notes.pdf" target="_blank">Click to download the PDF for my FDM notes</a>_

---

## Control Architecture Design

This part of the project deals with a very important question. Given a flight path, how does a drone go about executing it? Following the coursework of Mark Misin, a control architecture of a feedback linearization outer-loop and a model predictive inner-loop controller (MPC) has been employed.

![Control Architecture](/assets/img/navigator/controller-architecture.png)
_Control Architecture_

The feedback linearization, also known as “exact linearization”, is a non-linear control technique that transforms a non-linear system into a fully or partially decoupled linear one, without loss of any accuracy, so that linear control strategies may be used. Within this architecture this outer loop controller works as a position controller that computes the quadcopter orientation that is needed to get to the reference position provided by the planner.

The inner-loop model predictive control receives the target attitude angles to produce the most optimum control commands for the scenario. It does this by planning in advance for a specified number of timesteps known as the horizon period. A set of optimization objectives are defined which are then used to minimize a mathematical cost function, over this finite horizon period, to determine the best system input. This is done in a receding horizon fashion. The inner-loop runs at a higher frequency to try and catch the reference set by the outer-loop. For this we say that the inner-loop has dynamics stronger than the outer-loop.

The MPC controller needs equations of motion to make such predictions. If the attitude equations are visited in my course notes, then it is found that there are non-linearities present in them. To apply the formulations of a linear MPC controller to our non-linear set of equations, a two-fold process is used. First, the transfer matrix is simplified to simplify the EOMs from rates to Euler angles themselves. Secondly, linear parameter varying (LPV) is applied to put the EOMs into a linear format. The continuous set of equations are then discretised. Finally, a cost function is formulated, simplified, and solved for set goals.

All of these steps are mathematically intensive and thus, I am including my course notes in this section for anyone who may be interested in reading further. It is a good read for anyone new to optimal and quadrotor control and the notes provide reasoning for all design choices made.

![Controller Design Notes Preview](/assets/img/navigator/navigator-controller-design-notes-preview.png)
_<a href="{{site.url}}/assets/docs/navigator/navigator-controller-design-notes.pdf" target="_blank">Click to download the PDF for my controller design notes</a>_

---

## Towards Hardware Implementation

Once designed there is a need to evaluate the performance and assess the potential of the controller. Testing directly at a hardware level is a risky task as any unforeseen design flaw can lead to a hazard of damaging equipment, life, and surroundings. To avoid this, there is a very important step in control design process to perform Software in the Loop Simulations (SILS). Simulations are an excellent way to perform trade-studies, highlighting limitations, monitoring improvements, and enhancing realism of plant model and controller design by emulating flight conditions, scenarios, and disturbances that otherwise may not be possible to be replicated physically in a cost effective and reliable manner. After the design undergoes significant changes in this phase and a considerable confidence of the design is developed, the next step is to work towards its hardware implementation.

Developing a completely new controller and implementing it physically is an immensely challenging task; due to time constraints this isn’t within the scope of this project. It has been previously mentioned that the hardware platform chosen for this project is ETH Zurich’s Agilicious framework. Furthermore, the purpose of the analytically designed controller was to get a direct hand on with the important concepts that go into making one and better understand the adopted framework. Nonetheless, it would be exciting to see the engineered mathematics in action. For this I used the companion Python script provided by Mark Misin in his course and tweaked it to test a manoeuvring flight scenario.

![Python Trajectory Tracking](/assets/vid/navigator/controller-python-simulation.mp4)
_Model Predictive Control in action_

The hardware phase of the project is a major one. It’s an assimilation of a lot of skills including but not limited to Ubuntu Operating System, Robot Operating System, Docker, CAD Modelling, Design for Additive Manufacturing, Additive Manufacturing, Betaflight Firmware, and Jetson Nano. Through continuous troubleshooting a very strong understanding for the involved frameworks was developed. This phase although involved development of software and hardware in parallel, for the purposes of this blog I will be presenting first the hardware fabrication portion, followed by a software development portion, and then finally an integration and testing portion.

![Navigator](/assets/img/navigator/navigator-cyberpunk.gif)
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

![Wire Management](/assets/img/navigator/navigator-wire-management.jpg)
_Snug and Well Thought Out Wiring Scheme for High Speed Flights_

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

## Software

---

## Integration

---

## But Seriously, Why This Project?

---

## Further Reading

---
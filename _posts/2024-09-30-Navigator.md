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

The resulting framework consolidates over 15 years of research, spanning early demonstrations of vision-based autonomous flight to recent milestones achieved in human vs algorithmic piloting abilities. It highlights key challenges such as perception-to-action dependence, domain shifts, and sensor limitations, offering innovative solutions like hybrid simulation-real-world approaches. Additionally, the framework evaluates potential drone platforms suited for hardware implementation, and that are geared towards research and development. This work was presented as a conference paper at the Smart Mobility and Logistics Ecosystems conference at KFUPM, published through a peer-reviewed process. For a graphical overview of the design philosophy refer to the image below. For a detailed treatment of the subject, you can read my conference paper using this <a href="{{site.url}}" target="_blank">link</a>.

![Philosophy Flowchart](/assets/img/navigator/control-design-philosophy.jpg)
_Illustration of a general-purpose control design philosophy_

---

## Vehicle Dynamics Modelling

---

## Control Architecture Design

---

## Towards Hardware Implementation

---

## Hardware Implementation

---

## Future Work

---

## But Seriously, Why This Project?

---

## Further Reading

---
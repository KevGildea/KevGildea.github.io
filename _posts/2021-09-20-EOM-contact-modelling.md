---
title: "Computational modelling of a bouncing ball using differential equations of motion"
date: 2021-09-20
categories:
  - blog

tags:
  - Mechanics
  - Dynamics
  - Kinemaics
  - Physics
  - Numerical modelling
  - Mass-spring-damper model 
---

### Problem statement

Using differential equations of motion (EOM) we can describe the dynamics and kinematics of objects in motion. The most general equation of motion developed is Newton's second law of motion (i.e. F = ma). In this post I will describe how the equations of motion can be calculated and applied programmatically for a simple exemplar case of a falling and bouncing ball with one translational degree of freedom - i.e. the ball is bouncing perfectly perpindicular to the ground plane with no rotational component. 

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/Bouncing ball.gif" width="700">
</p>

### Defining the EOMs
We can split the problem up into two phases, where phase 1 involves the ball in freefall. Here the equation of motion is governed by the mass of the ball, and air resistance.

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/EOMs1.jpg">
</p>

In phase 2 we consider the contact/impact between the ball and the ground surface as an unforced mass-spring-damper model. Note that x<sup>pen</sup>(t) is the displacement in the contact phase (i.e. the penetration).


<p align="center">
  <img src="/assets/images/EOM-contact-modelling/EOMs2.jpg">
</p>


### Numerical integration of ODEs
Since each of the the equations of motion (for both phase 1 and phase 2) are in the form of a 2<sup>nd</sup> order ordinary differential we must apply the Runge-Kutta 4<sup>th</sup> order method to simply to the form of two coupled 1<sup>st</sup> order equations i.e. x<sup>1</sup>(t), and x<sup>2</sup>(t). To simplify the problem further we will disregard the effect of air resistance, i.e. set c<sub>drag</sub> to zero.

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/RungeKutta.png">
</p>


### Effect of varying parameters k and c



### Implications










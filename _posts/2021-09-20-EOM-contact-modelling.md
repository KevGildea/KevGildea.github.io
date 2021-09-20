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

In phase 2 we consider the contact/impact between the ball and the ground surface as an unforced mass-spring-damper model. Note that x<sub>pen</sub>(t) is the displacement in the contact phase (i.e. the penetration).


<p align="center">
  <img src="/assets/images/EOM-contact-modelling/EOMs2.jpg">
</p>


### Numerical integration of ODEs
Since each of the the equations of motion (for both phase 1 and phase 2) are in the form of a 2<sup>nd</sup> order ordinary differential we must apply the Runge-Kutta 4<sup>th</sup> order method to simply to the form of two coupled 1<sup>st</sup> order equations i.e. x<sub>1</sub>(t), and x<sub>2</sub>(t). To simplify the problem further we will disregard the effect of air resistance, i.e. set c<sub>drag</sub> to zero.

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/RungeKutta.png">
</p>


### Implementation

```matlab
function xdot  = ball(t,x);

global acc t_temp pos

k = 500; m  = 0.2; g = 9.81; h=0.2; r = 0.01; c=1;
xdot  = zeros(2,1);

%determine if penetration has occured
pen = (x(2) + r) - h; %compute penetetration for contact 
if pen <0 
    xdot(1) = g; xdot(2)  = x(1);
else xdot(1) = g - ((k*pen)/m) -((c*x(1))/m); xdot(2)  = x(1);
    
acc = [acc; xdot(1)];
t_temp = [t_temp; t];
pos= [pos; 0];

end

```

### Effect of varying parameters k and c

|         |     k=500 |     k=5,000 |     k=500,000 |
| c=0  |  ![](/assets/images/EOM-contact-modelling/k500c0.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c0.gif) |  ![](/assets/images/EOM-contact-modelling/k500000c0.gif) |
| c=5  |  ![](/assets/images/EOM-contact-modelling/k500c5.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c5.gif) | ![](/assets/images/EOM-contact-modelling/k500000c5.gif) | 
| c=10 |  ![](/assets/images/EOM-contact-modelling/k500c10.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c10.gif) |  ![](/assets/images/EOM-contact-modelling/k500000c10.gif) |

### Implications










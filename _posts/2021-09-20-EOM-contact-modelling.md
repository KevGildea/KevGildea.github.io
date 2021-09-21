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

EOM_contact_modelling.m
```matlab
close all; clear

%simulation of bouncing ball
global g k c m h r

% set parameter values
g = 9.81;k = 5000; c=5; m = 0.2; h=0.2; r = 0.01;

%set integration time interval, and time step
tspan = [0 2];
tstep = 1e-3;

%set initial conditions: velocity and displacement
X0 = [0  0];

%call ode23 function and feed relevant inputs
OPTIONS = odeset('MaxStep',tstep); %set max integration timestep
[tout,xout] = ode23('ball',tspan,X0,OPTIONS);

```

ball.m
```matlab
function xdot  = ball(t,x)

global g k c m h r

xdot  = zeros(2,1);

%determine if penetration has occured
pen = (x(2) + r) - h; %compute penetetration for contact

if pen <0 
    xdot(1) = g; xdot(2)  = x(1);
else xdot(1) = g - ((k*pen)/m) -((c*x(1))/m); xdot(2)  = x(1);

end

```

Choose nominal values for k, and c, i.e. k=5,000, and c=5, and plot position and velocity time histories.

POSITION & VELOCITY PLOTS
|  **Reference**  |  **Position and velocity plots** |
:-------------------------:|:-------------------------:
|![](/assets/images/EOM-contact-modelling/k5000c5.gif)  | ![](/assets/images/EOM-contact-modelling/k5000c5.png) |

Varying the drop height.
|  **h=0.35m**  |  **Position and velocity plots** |
:-------------------------:|:-------------------------:
  ![](/assets/images/EOM-contact-modelling/k5000c5h0.35.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c5h0.35.png) 

Adding an initial velocity to the ball.
|  **v=-1 m/s**  |  **Position and velocity plots** |
:-------------------------:|:-------------------------:
  ![](/assets/images/EOM-contact-modelling/k5000c5v-1.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c5v-1.png) 

Changing the mass and size of the ball
|  **m=0.5kg, r=0.08m**  |  **Position and velocity plots** |
:-------------------------:|:-------------------------:
  ![](/assets/images/EOM-contact-modelling/k5000c5m0.5r0.08.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c5m0.5r0.08.png) 

Dropping the ball in another gravitational environment.
|  **The Moon: g=1.62m/s/s**  |  **Position and velocity plots** |
:-------------------------:|:-------------------------:
  ![](/assets/images/EOM-contact-modelling/k5000c5g1.62.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c5g1.62.png) 


Effect of varying parameters k and c

|         |     k=500 |     k=5,000 |     k=500,000 |
:-------------------------:|:-------------------------:|:-------------------------:|:-------------------------:
| **c=0**  |  ![](/assets/images/EOM-contact-modelling/k500c0.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c0.gif) |  ![](/assets/images/EOM-contact-modelling/k500000c0.gif) |
| **c=5**  |  ![](/assets/images/EOM-contact-modelling/k500c5.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c5.gif) | ![](/assets/images/EOM-contact-modelling/k500000c5.gif) | 
| **c=10** |  ![](/assets/images/EOM-contact-modelling/k500c10.gif)  |  ![](/assets/images/EOM-contact-modelling/k5000c10.gif) |  ![](/assets/images/EOM-contact-modelling/k500000c10.gif) |

### Implications










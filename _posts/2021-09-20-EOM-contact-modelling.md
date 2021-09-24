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


Using differential equations of motion (EOMs) governed by Newton's 2<sup>nd</sup> law we can describe the dynamics and kinematics of objects in motion. In this post I describe how EOMs can be calculated and applied programmatically for a simple case of a falling and bouncing ball with one translational degree of freedom - i.e. a ball bouncing perfectly perpindicular to the ground plane with no rotational component. 

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/Bouncing ball.gif" width="700">
</p>

### Defining the equations of motion
We can split the problem up into two phases, where phase 1 involves the ball in freefall. Here the equation of motion is governed by gravitational force, and air resistance.

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/EOMs1.jpg">
</p>

In phase 2 we consider the contact/impact between the ball and the ground surface as an unforced mass-spring-damper model. Given appropriate model parameters, this kind of model can accurately represent overall impact/contact behaviour. We make the assumption that the ball is a rigid body that does not deform, and x<sub>pen</sub>(t) is the ground displacement in the contact phase (i.e. the penetration).


<p align="center">
  <img src="/assets/images/EOM-contact-modelling/EOMs2.jpg">
</p>


### Numerical integration of ordinary differential equations
Since each of the the EOMs (for both phase 1 and phase 2) are in the form of a 2<sup>nd</sup> order ordinary differential we apply a Runge-Kutta numerical integration approach. First, we need to simply the EOMs to the form of coupled 1<sup>st</sup> order equations i.e. x<sub>1</sub>(t), and x<sub>2</sub>(t). To simplify the problem further we will disregard the effect of air resistance, i.e. set c<sub>drag</sub> to zero.

<p align="center">
  <img src="/assets/images/EOM-contact-modelling/2ndODEto1stODE.png">
</p>

Specifically we apply the Matlab <a href="https://uk.mathworks.com/help/matlab/ref/ode23.html" target="_blank">ode23</a> function, which is an implementation of an explicit Runge-Kutta (2,3) pair of Bogacki and Shampine. There are other ODE solvers available in Matlab, for example <a href="https://uk.mathworks.com/help/matlab/ref/ode45.html" target="_blank">ode45</a>, which is a higher order method. For this simplified example the ode23 function is used as it is more computationally efficient.

### Implementation

The full code is available <a href="https://github.com/KevGildea/RotationTheory/blob/main/EOM-contact-modelling" target="_blank">here</a>.

main.m
```matlab
close all; clear

%simulation of bouncing ball
global g k c m h r

% set parameter values
g = 9.81;k = 5000; c=5; m = 0.2; h=0.2; r = 0.01;

%set integration time interval, and maximum time step
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

We would like to model a ball of mass 0.2kg, and radius 0.01m. For reference, we choose nominal values for the spring constant (k) and and damping constant (c) i.e. k=5,000, and c=5. 

|  Reference  |   |
:-------------------------:|:-------------------------:
![](/assets/images/EOM-contact-modelling/k5000c5.gif)  | ![](/assets/images/EOM-contact-modelling/k5000c5.png)

Effect of changing the drop height.

|   h=0.35m  |   |
:-------------------------:|:-------------------------:
![](/assets/images/EOM-contact-modelling/k5000c5h0.35.gif)  | ![](/assets/images/EOM-contact-modelling/k5000c5h0.35.png)

Effect of adding an initial velocity to the ball.

|   v=-1 m/s  |   |
:-------------------------:|:-------------------------:
![](/assets/images/EOM-contact-modelling/k5000c5v-1.gif)  | ![](/assets/images/EOM-contact-modelling/k5000c5v-1.png)

Effect of changing the mass and size of the ball.

|   m=0.5kg, r=0.08m   |   |
:-------------------------:|:-------------------------:
![](/assets/images/EOM-contact-modelling/k5000c5m0.5r0.08.gif)  | ![](/assets/images/EOM-contact-modelling/k5000c5m0.5r0.08.png)

Effect of the gravitational environment.

|   The Moon: g=1.62m/s/s   |   |
:-------------------------:|:-------------------------:
![](/assets/images/EOM-contact-modelling/k5000c5g1.62.gif)  | ![](/assets/images/EOM-contact-modelling/k5000c5g1.62.png)


Effects of varying parameters k and c.


:-------------------------:|:-------------------------:|:-------------------------:
| **Underdamped**  |  ![](/assets/images/EOM-contact-modelling/under-damped.gif)  |  ![](/assets/images/EOM-contact-modelling/under-damped.png) |
| **Critically damped**  |  ![](/assets/images/EOM-contact-modelling/critically-damped.gif)  |  ![](/assets/images/EOM-contact-modelling/critically-damped.png) |
| **Over damped** |  ![](/assets/images/EOM-contact-modelling/over-damped.gif)  |  ![](/assets/images/EOM-contact-modelling/over-damped.png) |

### Implications

In this post I have developed a physics simulation/computational model of a bouncing ball. Relationships between system parameters and the motion of a dropped ball are investigated, namely, the drop height, initial velocity, ball mass, ball size, and the ground surface stiffness and damping coefficient. Exploring this code and varying parameters may allow the user gain an understanding of the effects of contact characteristics.








---
title: "Euler axis solution space for mapping kinematic chains: A modified inverse kinematics approach"
#date: 2021-04-04
categories:
  - blog

tags:
  - Kinematics
  - Inverse Kinematics
  - Linear Algebra
  - Rotations

---

### Background

1. INTRODUCTION TO KINEMATIC CHAINS, AND INVERSE KINEMATICS
Generally, a kinematic chain can be described as a hierarchical chain of links and joints. Kinematic chains are described by 1) the locations and orientations of each of the joints, and 2) the heirarchy of the joints in the system, using a directed graph. 

https://en.wikipedia.org/wiki/Inverse_kinematics : inverse kinematics makes use of the kinematics equations to determine the joint parameters that provide a desired configuration (position and rotation) for each of the robot's end-effectors.
2. In this post I develop a method for mapping one kinematic chain (a) to another which does not contain any information on the orientations of the joints in the system.

ADD A FIGURE FOR THE MAPPED COMPLEX KINEMATIC CHAIN

In a previous post, I described how in SO(3) an infinite number of rotation matrices, or Euler/Screw axis-angle combinations can be applied to map one vector (a) onto another vector (b). However, the solution space is constrained such that the Euler/Screw axis must lay on the plane that bisects the vectors.

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig0.gif" width="700">
</p>

> For more infor see my blog post:
> ['Non-uniqueness of the Euler axis in vector mapping'](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/)

Now, if we assign an initial local coordinate system to vector a, for example, if we set choose it to be aligned with the global coordinate system then we can see the solution space for reorientation of this local coordinate system after mapping. 

WE DON'T NEED FIG1

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig1.gif" width="700">
</p>

If we choose a simpler example, with an initial local coordinate system for vector a where the Y axis (green) is alligned with the vector we can see that the solution space for reorientation of this local coordinate system after mapping is reduced. 

PLOT FIG 2 AS 2 SEPARATED VECTORS - DEMONSTRATINF THE USE CASE OF HAVING a VECTOR WITH NO ORIENTATION INFORMATION (b), AND ANOTHER WITH ORIENTATION INFORMATION (a) THAT WE WANT TO MAP.

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig2.gif" width="700">
</p>



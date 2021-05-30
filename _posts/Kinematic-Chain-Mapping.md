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
Generally, a kinematic chain can be described as a hierarchical system of links and joints. Kinematic chains are described by 1) the locations and orientations of each of the joints, and 2) the heirarchy of the joints in the system, using a directed graph. Inverse kinematics is an approach used to reorient a kinematic chain to achieve a desidered location and orientation for the final joint in the chain (referred to as the end-effector in robitics). This problem can be solved either analytically or numerically depending on the complexity of the chain, i.e. the Degrees of freedom of its joints. If the degrees of freedom of the chain exceeds the degrees of freedom of the end-effector then there exists an infinite number of solutions, and numerical optimization should be used. In this post I develop a method for mapping one kinematic chain (a) to another which does not contain any information on the orientations of the joints in the system. Where the chains must have the same number of joints and the same joint heirarchy, but may have differing and dsproportional link lengths. This is distict from traditional forms of inverse kinematics, in that the target involves mapping vectors throughout the chain, and does not specify degrees of freedom in terms of joint locations nor orientations.

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



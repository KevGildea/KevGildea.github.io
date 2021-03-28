---
title: "Optimization of joint reorientations for inverse kinematics"
#date: 2021-04-04
categories:
  - blog

tags:
  - Kinematics
  - Optimization
  - Linear Algebra
  - Rotations

---

### Background
In a [previous post](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/), I described how in SO(3) an infinite number of rotation matrices, or axis-angle combinations can be applied to map one vector (a) onto another vector (b). However, the solution space is constrained such that the Euler/Screw axis must lay on the plane that bisects the vectors.

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig0.gif" width="700">
</p>

Now, if we assign an initial local coordinate system to vector a, for example, if we set choose it to be aligned with the global coordinate system then we can see the solution space for reorientation of this local coordinate system after mapping. This can be used to represent the rotation of a joint.

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig1.gif" width="700">
</p>

In biomechanics, animation, robotics, and any field where kinematic chains are used to represent physical systems, there are often going to be constrains on joint reorientations, i.e. joint ranges of motion (ROMs). Constraints take the form of angular ranges about each of the initial local joint coordinate system's cardinal axes, which effectively eliminates certain ranges of Euler axes about which the rotation can take place, and Euler angles which can be performed. 







### Analytical solution

- Need for an approach for mapping dissimilar open kinematic chains (one without joint orientations)
- describe inverse kinematics
- vector mapping
- describe that it involves a nonlinear solution
- describe optimization


### Optimized solution


### Implications

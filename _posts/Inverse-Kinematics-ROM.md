---
title: "Joint reorientations and ranges of motion for inverse kinematics of simple open kinematic chains"
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
In biomechanics, animation, robotics, and any field where kinematic chains are used to represent physical systems, there are often going to be constraints on joint reorientations, i.e. joint ranges of motion (ROMs). Constraints take the form of angular ranges about each of the initial local joint coordinate system's cardinal axes, which effectively eliminates certain ranges of Euler axes about which the rotation can take place, and Euler angles which can be performed. This allows for the representation of physical joint types with differing degrees of freedom (DOF) e.g Free Joint: 6DOF, Ball/Spherical Joint: 3DOFs, Hardy Spicer/Universal Joint: 2DOFs, Hinge/Revolute Joint: 1DOF. 

In a previous post, I described how in SO(3) an infinite number of rotation matrices, or axis-angle combinations can be applied to map one vector (a) onto another vector (b). However, the solution space is constrained such that the Euler/Screw axis must lay on the plane that bisects the vectors.

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig0.gif" width="700">
</p>

> For more infor see my blog post:
> ['Non-uniqueness of the Euler axis in vector mapping'](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/)

Now, if we assign an initial local coordinate system to vector a, for example, if we set choose it to be aligned with the global coordinate system then we can see the solution space for reorientation of this local coordinate system after mapping. 

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig1.gif" width="700">
</p>

If we choose a simpler example, with an initial local coordinate system for vector a where the Y axis (green) is alligned with the vector we can see that the solution space for reorientation of this local coordinate system after mapping is reduced. 

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig2.gif" width="700">
</p>

If we want our rotation to act about the local Z axis (blue), then we can reduce the solution space further. Here we are choosing the local Z axis as the EUler axis, however, notice that no exact solution exists for this i.e. the the local Z axis does not lay on the Euler axis solution space.

 - Closest solution on the Euler axis solution space (fig3.png)
 #- Effect of choosing Z as the the rotation axis
 - We can also define a range of acceptable offsets from the Z axis (fig4.gif)
 - How does this relate to ROMs?



### Analytical solution

- Need for an approach for mapping dissimilar open kinematic chains (one without joint orientations)
- describe inverse kinematics
- vector mapping
- describe that it involves a nonlinear solution?
- describe optimization?


### Implications

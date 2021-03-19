---
title: "Non-uniqueness of the Euler axis in vector mapping"
date: 2021-03-21
categories:
  - blog

tags:
  - Linear Algebra
  - Rotations

---

### Background
This post requires some background knowledge of theoretical undepinnings of the 3D rotation group, or the special orthogonal group in three dimensions (i.e. SO(3)). This is an area of Linear Algebra in which special orthogonal matrices are used in 3 three-dimensional Euclidean space. This is widely used for representing object orientations in 3D space.
For example, the orientation of one coordinate system represented using basis vector e<sup>2</sup> can be represented wrt. another coordinate system e<sup>1</sup> by multiplying the latter by a 3x3 rotation matrix [A<sup>21</sup>]. If we know the orientations of both of these coordinate systems wrt. a 3<sup>rd</sup> coordinate system e<sup>0</sup>, i.e. the global coordinate system, then we can find [A<sup>21</sup>].


<p align="center">
  <img src="/assets/images/Skew-Axis-Vector-Mapping/fig1.png" width="700">
</p>


Euler's rotation theorem states that, in three-dimensional space, any displacement of a rigid body such that a point on the rigid body remains fixed, is equivalent to a single rotation about some axis that runs through the fixed point.


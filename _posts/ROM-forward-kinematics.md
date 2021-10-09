---
title: "Applying ranges of motion to constrain kinematic chains"
date: 2021-10-15
categories:
  - blog

tags:
  - Kinematics
  - Forward kinematics
  - Linear algebra
  - Rotations
  - Biomechanics
---

In this post I describe how rotation matrices can be constrained to produce physically plausible joint orientations, as a follow-up to the approach I developed for determining the <a href="https://kevgildea.github.io/blog/Kinematic-Chain-Mapping/" target="_blank">solution space for mapping kinematic chains</a>. In real world applications, e.g. robotics, biomechanics, kinematic chains often involve the use of physically constrained joints, i.e. joints with less than 6 degrees of freedom (DOF). Kinematic chains are often used in biomechanics applications, where joints positioned to approximate the human skeletal structure, and their rotations are rotations are kinematically constrained with differing degrees of freedom (e.g. free joint: 6DOF, ball/spherical joint: 3DOFs, hardy spicer/universal joint: 2DOFs, hinge/revolute joint: 1DOF). First, consider a joint in a 'reference' orientation.

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig1.png" width="1200">
</p>

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig2.png" width="1200">
</p>


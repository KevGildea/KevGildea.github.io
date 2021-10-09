---
title: "Applying degrees of freedom and ranges of motion to constrain kinematic chains in forward kinematics"
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

In this post I describe how rotation matrices can be constrained to produce physically plausible joint orientations in a kinematic chain, as a follow-up to the approach I developed for determining the <a href="https://kevgildea.github.io/blog/Kinematic-Chain-Mapping/" target="_blank">solution space for mapping kinematic chains</a>. In real-world applications, e.g. robotics, biomechanics, kinematic chains often involve the use of physically constrained joints. Kinematic chains are often used in biomechanics applications, where joints are positioned to approximate the human skeletal structure, and their rotations are kinematically constrained with differing degrees of freedom (e.g. free joint: 6DOF, ball/spherical joint: 3DOFs, hardy spicer/universal joint: 2DOFs, hinge/revolute joint: 1DOF), and ranges of motion. First, consider a joint in a 'reference' orientation.

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig1.png" width="1200">
</p>

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig2.png" width="1200">
</p>

IMPLEMENTATION WITH A SINGLE JOINT

DEGREES OF FREEDOM PLOTS:
1. Spherical joint 
2. Universal joint
3. Revolute joint
4. Bracket joint

RANGE OF MOTION PLOTS:
1. Revolute joint with a range of [0,pi]
2. Spherical joint with a range of [-pi/8,pi/8] between Y and y, and a range of [0,pi/2] between Y and x

IMPLEMENTATION IN A KINEMATIC CHAIN








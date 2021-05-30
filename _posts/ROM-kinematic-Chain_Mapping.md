---
title: "Solution space for inverse kinematics mapping of open kinematic chains"
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

In biomechanics, animation, robotics, and any field where kinematic chains are used to represent physical systems, there are often going to be constraints on joint reorientations, i.e. joint ranges of motion (ROMs). Constraints take the form of angular ranges about each of the local joint coordinate system's cardinal axes, which effectively eliminates certain ranges of Euler axes about which the rotation can take place, and Euler angles which can be performed. This allows for the representation of physical joint types with differing degrees of freedom (DOF) e.g Free Joint: 6DOF, Ball/Spherical Joint: 3DOFs, Hardy Spicer/Universal Joint: 2DOFs, Hinge/Revolute Joint: 1DOF.




If we want our rotation to act about the local Z axis (blue), then we can reduce the solution space further. Here we are choosing the local Z axis as the Euler axis, however, notice that no exact solution exists for this i.e. the the local Z axis does not lay on the Euler axis solution space.

 - Closest solution on the Euler axis solution space (fig3.png)
 - Effect of choosing Z as the the rotation axis
 - We can also define a range of acceptable offsets from the Z axis (fig4.gif)
 - How does this relate to ROMs?

EXTENDING THIS TO A KINEMATIC CHAIN USING INVERSE KINEMATICS

CREATE A KINEMATIC CHAIN WITH EACH JOINT TYPE IN SEQUENCE



### Analytical solution

- Need for an approach for mapping dissimilar open kinematic chains (one without joint orientations)
- describe inverse kinematics
- vector mapping
- describe that it involves a nonlinear solution?
- describe optimization?


### Implications

- COMPLEXITY INCREASES IN MORE COMPLEX OPEN KINEMATIC CHAINS (IS IT A NON-LINEAR SOLUTION)
- OPTIMIZATION MAY BE NEEDED?

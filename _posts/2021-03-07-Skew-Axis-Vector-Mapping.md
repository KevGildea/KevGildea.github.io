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


$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$


Euler's rotation theorem states that, in three-dimensional space, any displacement of a rigid body such that a point on the rigid body remains fixed, is equivalent to a single rotation about some axis that runs through the fixed point.


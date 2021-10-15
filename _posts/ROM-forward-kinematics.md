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

We know that there is an infinite Euler axis-angle solution space for mapping a vector a to another vector b, however, the axes are constrained to be on the plane that bisects the vectors, such that the normalised vectors are symmetric to the plane (as described <a href="https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/" target="_blank">here</a>). 

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig4.gif" width="1200">
</p>

If we set vector a to be aligned with the local x axis, and vector b aligned with the local y axis, then we can constrain the solution space for a joint which only allows rotation about its local z axis (which obviously is within the Euler axis solution space). We do this by specifying that the rotation matrix must have a value of a<sub>33</sub> = 1.

| Spherical joint           |  Revolute joint (local z-axis) |
:-------------------------:|:-------------------------:
![](/assets/images/ROM-forward-kinematics/fig5.gif)  |  ![](/assets/images/ROM-forward-kinematics/fig6.gif)
![](/assets/images/ROM-forward-kinematics/fig2.png)  |  ![](/assets/images/ROM-forward-kinematics/fig3.png)

As you can see, there are two solutions, one with a negative rotation of -1.57 degrees about an axis in the negative z direction, and another positive rotation of 1.57 about the positive z diretion, both resulting with identical rotation matrices, and a value of a<sub>33</sub> = 1. Therefore, we can halve the solution space.

```python
def Vector_mapping_Euler_Axis_Space(vec1, vec2):
    """ Calculate all rotation matrices that map vector a to align with vector b"""
    a, b = (vec1 / np.linalg.norm(vec1)), (vec2 / np.linalg.norm(vec2))
    p1 = np.array([0,0,0])
    p2 = b / np.linalg.norm(b) + (a / np.linalg.norm(a))
    p3 = np.cross(a, b) / np.linalg.norm(np.cross(a, b))
    n=[]
    # create a list of candidate Euler axes (discritised to 1 degree)
    for i in range(0,179,1):
        Φ=np.radians(i)
        x_Φ=p1[0]+np.cos(Φ)*(p2[0]-p1[0])+np.sin(Φ)*(p3[0]-p1[0])
        y_Φ=p1[1]+np.cos(Φ)*(p2[1]-p1[1])+np.sin(Φ)*(p3[1]-p1[1])
        z_Φ=p1[2]+np.cos(Φ)*(p2[2]-p1[2])+np.sin(Φ)*(p3[2]-p1[2])
        n_Φ=[x_Φ,y_Φ,z_Φ]
        n.append(n_Φ / np.linalg.norm(n_Φ))
    # project vectors to form a cone around the Euler axis, and determine required angle for mapping
    rotation_matrices=[]
    Euler_axes=[]
    Euler_angles=[]
    for i in range(len(n)):
        Euler_axes.append(n[i])
        if i==0:
            θ = np.radians(180)
        else:
            a_Φ, b_Φ = (np.cross(a,n[i]) / np.linalg.norm(np.cross(a,n[i]))), (np.cross(b,n[i]) / np.linalg.norm(np.cross(b,n[i])))
            θ = np.arccos(np.dot(a_Φ,b_Φ))
            θ = θ*np.sign(np.dot(n[i], np.cross(a_Φ,b_Φ)))
        Euler_angles.append(θ)
        rotation_matrices.append(np.array([[n[i][0]**2+(n[i][1]**2+n[i][2]**2)*(np.cos(θ)),n[i][0]*n[i][1]*(1-np.cos(θ))-n[i][2]*np.sin(θ),n[i][0]*n[i][2]*(1-np.cos(θ))+n[i][1]*np.sin(θ)],
                                          [n[i][0]*n[i][1]*(1-np.cos(θ))+n[i][2]*np.sin(θ),n[i][1]**2+(n[i][0]**2+n[i][2]**2)*(np.cos(θ)),n[i][1]*n[i][2]*(1-np.cos(θ))-n[i][0]*np.sin(θ)],
                                          [n[i][0]*n[i][2]*(1-np.cos(θ))-n[i][1]*np.sin(θ),n[i][1]*n[i][2]*(1-np.cos(θ))+n[i][0]*np.sin(θ),n[i][2]**2+(n[i][0]**2+n[i][1]**2)*(np.cos(θ))]]))
    
    return Euler_axes, Euler_angles, rotation_matrices
```

| Spherical joint           |  Revolute joint (local z-axis) |
:-------------------------:|:-------------------------:
![](/assets/images/ROM-forward-kinematics/fig7.gif)  |  ![](/assets/images/ROM-forward-kinematics/fig8.gif)
![](/assets/images/ROM-forward-kinematics/fig2.png)  |  ![](/assets/images/ROM-forward-kinematics/fig3.png)

Consider a universal/hardy spicer joint with 2DOF, involving sequential rotations about its local x axis and local y axes.

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig9.png" width="1200">
</p>

Combining these rotations:

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig10.png" width="1200">
</p>

We can use this to constrain the degrees of freedome of the joint, and specify joint ranges of motion, effectively reducing the Euler axis solution space. 

First, consider a joint we would like to represent the shoulder.

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig11.png" width="1200">
</p>



| Spherical joint           |  Spherical joint with ROMs |
:-------------------------:|:-------------------------:
![](/assets/images/ROM-forward-kinematics/fig12.gif)  |  ![](/assets/images/ROM-forward-kinematics/fig14.gif)
![](/assets/images/ROM-forward-kinematics/fig13.png)  |  ![](/assets/images/ROM-forward-kinematics/fig15.png)










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

**REMOVE**
<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig4.gif" width="1200">
</p>

## 1DOF joint with ROM 

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

## 2DOF joint with ROMs
We can use the direction cosines to constrain the degrees of freedom of the joint, and specify joint ranges of motion, effectively reducing the Euler axis solution space. 

First, consider a joint we would like to represent the shoulder. 

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig11.png" width="1200">
</p>

If we would like to map the upper arm (vector a) to point in the direction of vector b, then there are an infinite number of possible solutions, where as before, for a spherical joint with no constraints the Euler axis is constrained to be on the plane that bisects the vectors, such that the normalised vectors are symmetric to the plane - all resulting in different resultant shoulder joint orientations. We would like to reduce the solution space by describing the joint as a universal/hardy spicer joint with 2DOF, and physically plausable ranges of motion about the y and z axes when performing sequential rotations. 

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig9.png" width="1200">
</p>

Combining these rotations:

<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig10.png" width="1200">
</p>

Finding the Euler axis-angle solution space as follows, and constraining using the 2DOF rotation matrix, and physically plausable ranges of motion for the sequential rotations:
<p align="center">
  <img src="/assets/images/ROM-forward-kinematics/fig12.png" width="1200">
</p>

There is a trade-off between the step size taken in computing the Euler axis-angle solution space (which negatively affects compute time, and positively effects accuracy), and the 'closeness' tolerance required to accept a rotation matrix as a 2DOF rotation (higher tolerance results in better identification of solutions). 

| | a<sub>32</sub> tol: 1e-3           | a<sub>32</sub> tol: 1e-4           |  a<sub>32</sub> tol: 1e-5   |
:-------------------------:|:-------------------------:|:-------------------------:|:-------------------------:
**180 steps**  |![](/assets/images/ROM-forward-kinematics/1801e-3.gif)  |  ![](/assets/images/ROM-forward-kinematics/1801e-4.gif)  |  ![](/assets/images/ROM-forward-kinematics/1801e-5.gif)
**1,800 steps**   |![](/assets/images/ROM-forward-kinematics/18001e-3.gif)  |  ![](/assets/images/ROM-forward-kinematics/18001e-4.gif)  |  ![](/assets/images/ROM-forward-kinematics/18001e-5.gif)
**18,000 steps**   |![](/assets/images/ROM-forward-kinematics/180001e-3.gif)  |  ![](/assets/images/ROM-forward-kinematics/180001e-4.gif)  |  ![](/assets/images/ROM-forward-kinematics/180001e-5.gif)

A tolerance of 1e-3 is chosen for a<sub>32</sub>,and a step size of 20,000 is chosen for the Euler axis-angle solution space. For context, a tolerance of 1e-3 for a<sub>32</sub> corresponds to a tolerance of 0.057 degrees between the z axis in e<sup>2</sup> and the y axis e<sup>1</sup>, i.e. a high degree of accuracy.

| | b vectors with successful mapping within the ROM           |  resultant joint orientations within the ROM           |
:-------------------------:|:-------------------------:|:-------------------------:
**20,000 steps**  |![](/assets/images/ROM-forward-kinematics/20001e-3b.gif)  |  ![](/assets/images/ROM-forward-kinematics/20001e-3axes.gif)





## Mathematical proof as to why there is a single solition for a 2DOF (universal) joint

## 3DOF joint with ROMs



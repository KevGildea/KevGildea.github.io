---
title: "Non-uniqueness of the Euler axis in vector mapping"
date: 2021-03-19
categories:
  - blog

tags:
  - Linear Algebra
  - Rotations

---

### Background
This post requires some background theoretical knowledge of the 3D rotation group, or the special orthogonal group in three dimensions (SO(3)). This is an area of Linear Algebra in which special orthogonal matrices are used in three-dimensional Euclidean space. This group is widely used for representing object orientations.

For this task, basis vectors are used to describe the directions of the cardinal axes of the object's local coordinate system. For example, for object '0' the local coordinate system can be described as follows using basis vectors; in this case the object is alligned witht the global coordinate system, so the basis vector system is equal to the identity matrix (I), and each of the basis vectors ({e<sub>1</sub>}<sup>0</sup>, {e<sub>2</sub>}<sup>0</sup>, and {e<sub>3</sub>}<sup>0</sup>) extend 1 unit from the origin along each of the cardinal axes.

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig0.png" width="700">
</p>

Furthermore, the orientation of one coordinate system represented using basis vector e<sup>2</sup> can be represented wrt. another coordinate system e<sup>1</sup> by multiplying the latter by a 3x3 rotation matrix [A<sup>21</sup>]. If we know the orientations of both of these coordinate systems wrt. a 3<sup>rd</sup> coordinate system e<sup>0</sup>, i.e. the global coordinate system, then we can find [A<sup>21</sup>].


<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig1.png" width="700">
</p>

Euler's rotation theorem states that, in three-dimensional space, any displacement of a rigid body such that a point on the rigid body remains fixed, is equivalent to a single rotation about some axis that runs through the origin of the coordinate system. This axis is called the Euler axis, or the Screw axis.

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig2.png" width="700">
</p>

### Mapping of two vectors
Now, consider the case where instead of having two complete coordinate systems represented by basis vectors, we only have two vectors a and b, which we want to use to represent a rotation between the two coordinate systems. Clearly, there will not be a unique solution to this problem so we need to define the Screw axis about which we rotate. 

Two obvious candidate axes that can be chosen for this are:
1. the cross product of the vectors, which will be mutually perpindicular to both a and b, or
2. the sum of the normalised vectors a and b, which symmetrically bisects a and b.

choosing:
```python
a=[0.1,0.3,0.4]
b=[0.3,0.1,0.2]
```

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig3.png" width="700">
</p>

Implementation of cross product approach (axb):

```python
def Vector_mapping_cross_product(vec1, vec2):
    """ Calculate the rotation matrix that maps unit vector a to align with unit vector b about an axis aligned with the cross product"""
    a, b = vec1 / np.linalg.norm(vec1), vec2 / np.linalg.norm(vec2)
    n = np.cross(a, b) / np.linalg.norm(np.cross(a, b))
    rotation_matrix = np.array([[n[0]**2+(n[1]**2+n[2]**2)*(np.dot(a, b)),n[0]*n[1]*(1-np.dot(a, b))-n[2]*np.linalg.norm(np.cross(a, b)),n[0]*n[2]*(1-np.dot(a, b))+n[1]*np.linalg.norm(np.cross(a, b))],
                                [n[0]*n[1]*(1-np.dot(a, b))+n[2]*np.linalg.norm(np.cross(a, b)),n[1]**2+(n[0]**2+n[2]**2)*(np.dot(a, b)),n[1]*n[2]*(1-np.dot(a, b))-n[0]*np.linalg.norm(np.cross(a, b))],
                                [n[0]*n[2]*(1-np.dot(a, b))-n[1]*np.linalg.norm(np.cross(a, b)),n[1]*n[2]*(1-np.dot(a, b))+n[0]*np.linalg.norm(np.cross(a, b)),n[2]**2+(n[0]**2+n[1]**2)*(np.dot(a, b))]])
    return rotation_matrix
```

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig5.PNG" width="700">
</p>

Implementation of bisecting vector approach (a+b):
```python
def Vector_mapping_bisect(vec1, vec2):
    """ Calculate the rotation matrix that maps unit vector a to align with unit vector b about an axis aligned with norm(a) + norm(b)"""
    a, b = vec1 / np.linalg.norm(vec1), vec2 / np.linalg.norm(vec2)
    n = (a+b) / np.linalg.norm(a+b)
    θ = math.pi
    rotation_matrix = np.array([[n[0]**2+(n[1]**2+n[2]**2)*(np.cos(θ)),n[0]*n[1]*(1-np.cos(θ))-n[2]*np.sin(θ),n[0]*n[2]*(1-np.cos(θ))+n[1]*np.sin(θ)],
                                [n[0]*n[1]*(1-np.cos(θ))+n[2]*np.sin(θ),n[1]**2+(n[0]**2+n[2]**2)*(np.cos(θ)),n[1]*n[2]*(1-np.cos(θ))-n[0]*np.sin(θ)],
                                [n[0]*n[2]*(1-np.cos(θ))-n[1]*np.sin(θ),n[1]*n[2]*(1-np.cos(θ))+n[0]*np.sin(θ),n[2]**2+(n[0]**2+n[1]**2)*(np.cos(θ))]])
    return rotation_matrix
```

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig6.PNG" width="700">
</p>


Now, we can use the two points obtained from the a+b approach and the axb approach along with the origin to define the plane that contains all possible rotation axes.

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig4.gif" width="700">
</p>

Or, more appropriately, we can define the Euler axis space as all unit vectors on the plane.

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig10.gif" width="700">
</p>

The axis-angle combination can be visualised by looking down the chosen axis to the origin - with the projection of the vectors a and b onto this plane the required angle becomes clear. This rotation can be visualised as a rotation of a right circular cone about its axis, where the vectors norm(a) and norm(b) lay on the surface of the base pointing outwards from the centre (i.e. the origin) to the directrix, and n points outwards from the centre of the base to the apex.

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig7.PNG" width="700">
</p>

Implementation of user-defined axis approach:
```python
def Vector_mapping_UDaxis(vec1, vec2): 
    """ Calculate all rotation matrices that map unit vector a to align with unit vector b"""
    a, b = (vec1 / np.linalg.norm(vec1)), (vec2 / np.linalg.norm(vec2))
    p1 = np.array([0,0,0])
    p2 = b / np.linalg.norm(b) + (a / np.linalg.norm(a))
    p3 = np.cross(a, b) / np.linalg.norm(np.cross(a, b))
    n=[]
    # create a list of candidate Euler axes (discritised to 1 degree)
    for i in range(0,360,1):
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
        a_Φ, b_Φ = (np.cross(a,n[i]) / np.linalg.norm(np.cross(a,n[i]))), (np.cross(b,n[i]) / np.linalg.norm(np.cross(b,n[i])))
        θ = np.arccos(np.dot(a_Φ,b_Φ))
        θ = θ*np.sign(np.dot(n[i], np.cross(a_Φ,b_Φ)))
        Euler_angles.append(θ)
        rotation_matrices.append(np.array([[n[i][0]**2+(n[i][1]**2+n[i][2]**2)*(np.cos(θ)),n[i][0]*n[i][1]*(1-np.cos(θ))-n[i][2]*np.sin(θ),n[i][0]*n[i][2]*(1-np.cos(θ))+n[i][1]*np.sin(θ)],
                                    [n[i][0]*n[i][1]*(1-np.cos(θ))+n[i][2]*np.sin(θ),n[i][1]**2+(n[i][0]**2+n[i][2]**2)*(np.cos(θ)),n[i][1]*n[i][2]*(1-np.cos(θ))-n[i][0]*np.sin(θ)],
                                    [n[i][0]*n[i][2]*(1-np.cos(θ))-n[i][1]*np.sin(θ),n[i][1]*n[i][2]*(1-np.cos(θ))+n[i][0]*np.sin(θ),n[i][2]**2+(n[i][0]**2+n[i][1]**2)*(np.cos(θ))]]))
    
    return Euler_axes, Euler_angles, rotation_matrices
```


Examples of valid mapping for arbitrarily chosen axes on the plane (it works!):

<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig8.PNG" width="700">
</p>


<p align="center">
  <img src="/assets/images/Euler-Axis-Vector-Mapping/fig9.PNG" width="700">
</p>



### Implications
With a lack of complete basis vector representation for the two coordinate systems, there are an infinite number of rotation matrices, or axis-angle combinations that can be applied to achieve a desired vector mapping. However, here I have demonstrated that candidate Euler/Screw axes are constrained to be on the plane that bisects the vectors, such that the normalised vectors are symmetric to the plane. With this knowledge we can programatically solve for all possible vector mapping solutions. 


The full code is available [here](https://github.com/KevGildea/RotationTheory/blob/fe2cb2b7230284d3944cd7d76d5fd2341a96d3b6/Non-uniqueness%20of%20the%20Euler%20axis%20in%20vector%20mapping/Non_uniqueness_Euler_axis_vector_mapping.py).


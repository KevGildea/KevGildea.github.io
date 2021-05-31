---
title: "Solution space for mapping kinematic chains: A modified inverse/forward kinematics approach"
#date: 2021-05-30
categories:
  - blog

tags:
  - Kinematics
  - Inverse Kinematics
  - Linear Algebra
  - Rotations

---

### Kinematic chains
Generally, a kinematic chain can be described as a hierarchical system of links and joints. Kinematic chains are described by 1) the locations and orientations of each of the joints, and 2) the heirarchy of the joints in the system, e.g. using a directed graph. Inverse kinematics is an approach used to reorient an open kinematic chain (i.e. no looping) to achieve a desidered location and orientation for the final joint in the chain (referred to as the end-effector in robotics). This problem can be solved either analytically or numerically depending on the complexity of the chain, i.e. the Degrees of freedom of the system. If the degrees of freedom of the chain exceeds the degrees of freedom of the end-effector then there exists an infinite number of solutions, and numerical optimization should be used. In this post I develop a method for calculating the solution space for mapping one kinematic chain (a) to another (b), where the latter does not contain any information on joint orientations. The chains must have the same number of joints and the same joint heirarchy, but may have differing and disproportional link lengths. This is distinct from traditional forms of inverse kinematics, in that the target involves mapping vectors throughout the chain, and does not specify degrees of freedom in terms of joint locations nor orientations.

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig0.png" width="700">
</p>


### Vector mapping
In a previous post, I described how in SO(3) an infinite number of rotation matrices, or Euler/Screw axis-angle combinations can be applied to map one vector (a) onto another vector (b). However, the solution space is constrained such that the Euler/Screw axis must lay on the plane that bisects the vectors.

> For more information see my blog post:
> ['Non-uniqueness of the Euler axis in vector mapping'](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/)


If we assign an initial local coordinate system to vector a, for example, if we set it to be aligned with the global coordinate system then we can see the Euler axis-angle solution space for reorientation of this local coordinate system. 

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig1.gif" width="700">
</p>

Alternatively, we can choose a simpler orientation, with an initial local coordinate system for vector a where the Y axis (green) is alligned with the vector. In this case, the solution space is more easily visualised. 

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig2.gif" width="700">
</p>

### Definining a kinematic chain and applying forward kinematics 

We can define a simple open kinematic chain 'a' using a parent-child convention, where DOFs of child joints are expressed with respect to the parent joint DOFs; i.e. the position of the child joint is expressed as a vector in the coordinate system of the parent joint, and the orientation of the child joint is expressed as a rotation matrix which specifies the orientation of the child joint wrt. the parent joint's orientation. This is the conventional approach for defining kinematic chains because it allows for various kinematic and dynamic operations to be performed. Firstly, we can consider a simple open kinematic chain, where the joints are arranged in series with no forking (i.e. all joints in the chain have a maximum of one child joint), where joint 0 is the root joint which is connected to the reference space. [See here](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/#the-3d-rotation-group) for a brief overview of some relevant theory for the 3D rotation group.

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig6.png" width="700">
</p>

We can use this information to calculate the joint positions and orientations in the global coordinate system i.e. forward kinematics.

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig7.png" width="700">
</p>

Using this knowledge we can programatically define a kinematic chain and plot it in the global coordinate system using forward kinematics: 

```python
chain_a.append(['jnt_a0', np.array([[ 1, 0, 0],
                                    [ 0, 1, 0],
                                    [ 0, 0, 1]]),
                          np.array([0,0.2,0])])
chain_a.append(['jnt_a1', np.array([[ 0, 1, 0],
                                    [ 0, 0, 1],
                                    [ 1, 0, 0]]),
                          np.array([0,0.2,0])])
chain_a.append(['jnt_a2', np.array([[ 1, 0, 0],
                                    [ 0, 0, 1],
                                    [ 0, 1, 0]]),
                          np.array([0.5,0,0])])
chain_a.append(['jnt_a3', np.array([[ 0, 0, 1],
                                    [ 1, 0, 0],
                                    [ 0, 1, 0]]),
                          np.array([0,0.2,0])])
chain_a.append(['jnt_a4', np.array([[ 1, 0, 0],
                                    [ 0, 0, 1],
                                    [ 0, 1, 0]]),
                          np.array([0,0,0.2])])
```
In order to perform kinematic operation on the chain we must aslo specify its heirarchical structure using a directed graph. 
```python
dir_graph = {0: [1],
             1: [2],
             2: [3],
             3: [4]}
```

For implementation of forward kinematics we must use the directed graph to define the path for each joint (i.e. a list of all joints on the path from the root joint).

```python
def jnt_path(graph, start, end, path=[]):
    """ list all joints on the path to a specified joint"""
    path = path + [start]
    if start == end:
        return path
    if not start in graph:
        return None
    for node in graph[start]:
        if node not in path:
            newpath = jnt_path(graph, node, end, path)
            if newpath: return newpath
    return None
```
The forward kinematics solution first defines the reference space to be at (0,0,0) with an identity matrix orientation, then reads in the locally defined joint DOFs for each joint and sequentially calculates the global DOFs along the path to the joint.

```python
def FK_local2global(chain, dir_graph): 
    """ perform forward kinematics to to convert locally defined joint DOFs into the global coordinate system"""
    ref_space_ori = np.array([[1, 0, 0],
                              [0, 1, 0],
                              [0, 0, 1]])
    ref_space_pos = np.array([0, 0, 0])
    oris=[]
    poss=[]
    for i in range (len(chain)):
        path = jnt_path(dir_graph, 0, i)
        ori = ref_space_ori
        pos = ref_space_pos
        for j in path:
            pos=pos + ori @ chain[j][2]
            ori=ori @ chain[j][1]
        oris.append(ori)
        poss.append(pos)
    
    return oris, poss
```
Plotting the kinematic chain in the global coordinate sysem:

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig8.PNG" width="700">
</p>

Since we use the path to each joint from the directed graph, this approach also works for more complex kinematic chains with branching (i.e. where joints may have multiple children).

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig9.PNG" width="700">
</p>

### Solution space for mapping kinematic chains

The goal is to use kinematics knowledge to extend the [vector mapping method](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/#mapping-of-two-vectors) I previously developed for use on a kinematic chain. Specifically, I would like to develop a method for calculating the solution space for mapping one kinematic chain (a) to another (b), where the latter does not contain any information on joint orientations. The chains must have the same number of joints and the same joint heirarchy, but may have differing and disproportional link lengths. This will require a kinematical approach involving sequential calculations of the Euler axis-angle solution space for each joint throughout the chain. The problem is complicated by the fact that the Euler axis-angles in upchain joints affect the orientations and the resulting solution spaces for mapping downchain joints. 

Firstly, we can use the simple open kinematic chain defined above. We define chain b using only joint positions in the global coordinate system, and use same directed graph as chain a which we previously defined.

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig3.gif" width="700">
</p>

MATHEMATICALLY DESCRIBE 'def IK_simple_open_chain'

Firstly, we must define our [vector mapping method](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/#mapping-of-two-vectors) which will be called upon sequentially throughout the mapping process.

```python
def Vector_mapping_Euler_Axis_Space(vec1, vec2): 
    """ Calculate all rotation matrices that map vector a to align with vector b"""
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
        if θ != θ: # if θ is NaN
            rotation_matrices.append(np.array([[ 1, 0, 0],
                                               [ 0, 1, 0],
                                               [ 0, 0, 1]]))
        else:
            rotation_matrices.append(np.array([[n[i][0]**2+(n[i][1]**2+n[i][2]**2)*(np.cos(θ)),n[i][0]*n[i][1]*(1-np.cos(θ))-n[i][2]*np.sin(θ),n[i][0]*n[i][2]*(1-np.cos(θ))+n[i][1]*np.sin(θ)],
                                        [n[i][0]*n[i][1]*(1-np.cos(θ))+n[i][2]*np.sin(θ),n[i][1]**2+(n[i][0]**2+n[i][2]**2)*(np.cos(θ)),n[i][1]*n[i][2]*(1-np.cos(θ))-n[i][0]*np.sin(θ)],
                                        [n[i][0]*n[i][2]*(1-np.cos(θ))-n[i][1]*np.sin(θ),n[i][1]*n[i][2]*(1-np.cos(θ))+n[i][0]*np.sin(θ),n[i][2]**2+(n[i][0]**2+n[i][1]**2)*(np.cos(θ))]]))
    
    return Euler_axes, Euler_angles, rotation_matrices
```

Next, we 
```python
def simple_open_chain_mapping(chain_a, chain_b, dir_graph): # Consider renaming Could more aptly be described as a modified forward kinematics approach?
    """ perform inverse kinematics to map a simple kinematic chain a (an open chain without forking) to chain b, which must have the same directed graph"""
    ori_a, pos_a = FK_local2global(chain_a,dir_graph)
    _, pos_b = FK_local2global(chain_b,dir_graph)

    pos_a= pos_a - chain_a[0][2]
    pos_b= pos_b - chain_b[0][2]
    
    #convert directed graph for use in nx
    dir_graph = nx.DiGraph(dir_graph)

    repos_a_EAS=[]
    reori_a_EAS=[]
    Euler_axis=[]
    Euler_axes=[]

    for i in range(1,360,1): 
        reori_a=copy.deepcopy(ori_a)
        repos_a=copy.deepcopy(pos_a)
        Euler_axis=[]
        for j in range(len(chain_a)):
            downchain = list(nx.nodes(nx.dfs_tree(dir_graph, j))) # list of index values for j and all joints down chain
            if j < len(chain_a)-1:
                ROTM= Vector_mapping_Euler_Axis_Space(repos_a[j+1]-repos_a[j], pos_b[j+1]-pos_b[j])[2][i]
                Euler_axis.append(Vector_mapping_Euler_Axis_Space(repos_a[j+1]-repos_a[j], pos_b[j+1]-pos_b[j])[0][i])
            for k in range(len(downchain)):
                if downchain[0] != downchain[-1]:
                    reori_a[downchain[k]]= ROTM @ reori_a[downchain[k]]
                if downchain[k] != downchain[-1]:
                    repos_a[downchain[k+1]]= repos_a[j] + ROTM @ (repos_a[downchain[k+1]]-repos_a[j])
        repos_a= repos_a + chain_a[0][2]

        repos_a_EAS.append(repos_a)
        reori_a_EAS.append(reori_a)
        Euler_axes.append(Euler_axis)

    return reori_a_EAS, repos_a_EAS, Euler_axes
```
THE FUNCTION IS NOT OUTPUTTING THE FULL SOLUTION SPACE - EULER AXES-ANGLE SOLUTION SPACE IS ONLY BEING OUTPUT FOR THE NUMBER OF SOLUTIONS SPECIFIED FOR THE FIRST JOINT e.g. 'for i in range(1,360,5):' results in a shape of (72, 4, 3) for 'Euler_axes'

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig4.gif" width="700">
</p>


DESCRIBE THE MATHEMATICS OF EXTENDING THIS TO A COMPLEX KINEMATIC CHAIN

<p align="center">
  <img src="/assets/images/Kinematic-Chain-Mapping/fig5.gif" width="700">
</p>

Implementation of a modified inverse kinematics approach for mapping a complex kinematic chain:

```python
def IK_complex_open_chain(chain_a, chain_b, dir_graph): 
    """ perform inverse kinematics to map a complex kinematic chain a (an open chain with branching) to chain b, which must have the same directed graph"""


    return 

```

### Implications
The method developed here does not fit the definitions of forward kinematics nor inverse kinematics in that it.... 

---
title: "Kinematic differential equations"
date: 2021-10-06
categories:
  - blog

tags:
  - Kinematics
  - Physics
  - Numerical modelling
  - Euler integration
  - Linear algebra
  - Rotations
---


We can use kinematic differential equations to determine both 1) where an object will be and 2) what orientation it will have after a specified amount of time. In this post I describe an example that can be considered representative of a self propelling sphere in a vacuum with no gravitational effect (i.e. dynamics are not considered), initialised with angular and linear velocity.

<p align="center">
  <img src="/assets/images/Kinematic-Differential-Equations/KDEpos.gif" width="1200">
</p>
<p align="center">
  <img src="/assets/images/Kinematic-Differential-Equations/KDEori.gif" width="1200">
</p>

### Euler Integration

<p align="center">
  <img src="/assets/images/Kinematic-Differential-Equations/fig1.png" width="1200">
</p>

<p align="center">
  <img src="/assets/images/Kinematic-Differential-Equations/fig2.png" width="1200">
</p>

<p align="center">
  <img src="/assets/images/Kinematic-Differential-Equations/KDEoriScrew.gif" width="1200">
</p>


MATHS FOR

<p align="center">
  <img src="/assets/images/Kinematic-Differential-Equations/KDEposV.gif" width="1200">
</p>

### Implementation

'''python
# Function for performing Euler integration on the rotation matrix
def EulerInt(A0,ω,r0,v,t_step,t_end):
    At=A0
    Ats=[]
    rt=r0
    rts=[]
    ω_skewsym = np.array([[0, -ω[2], ω[1]],
                         [ω[2], 0,-ω[0]],
                         [-ω[1], ω[0], 0]])
    for t in range(int(t_end/t_step)):
        At = At + t_step*(-ω_skewsym @ At)
        Ats.append(At)
        rt = rt + t_step*(At@v)
        rts.append(rt)
    return Ats,rts
'''

MATHS FOR MAKING MATRIX ORTHOGONAL AND CHECKING IF IT IS A VALID ROTATION MATRIX

'''python
def isRotationMatrix(M):
    tag = False
    I = np.identity(M.shape[0])
    #if np.all((np.matmul(M, M.T)) == I) and (np.linalg.det(M)==1): tag = True
    print(np.matmul(M, M.T))
    check1 = np.isclose((np.matmul(M, M.T)), I, atol=1e-5)
    print(np.linalg.det(M))
    check2 = isclose(np.linalg.det(M),1,abs_tol=1e-5)
    if check1.all()==True and check2==True: tag = True
    return tag
'''

MUST BE INCLDED IN IMPLEMENTATION

'''python
# Function for performing Euler integration on the rotation matrix
def EulerInt(A0,ω,r0,v,t_step,t_end):
    At=A0
    Ats=[]
    rt=r0
    rts=[]
    ω_skewsym = np.array([[0, -ω[2], ω[1]],
                         [ω[2], 0,-ω[0]],
                         [-ω[1], ω[0], 0]])
    for t in range(int(t_end/t_step)):
        At = At + t_step*(-ω_skewsym @ At)
        correction_matrix = (3*np.array([[1, 0, 0],[0, 1, 0],[0, 0, 1]]) - (At @ At.T))/2 # correction matrix to ensure that the rotation matrix is orthogonal
        At = correction_matrix @ At
        if isRotationMatrix(At)==False: # if the matrix does not qualify as a rotation matrix (within a tolerance) then output an error
            sys.exit('Error: Chosen integration time step is too large - try a smaller value (generally a step of <=1e-2 is recommended)')
        Ats.append(At)
        rt = rt + t_step*(At@v)
        rts.append(rt)
    return Ats,rts
'''

### Implications




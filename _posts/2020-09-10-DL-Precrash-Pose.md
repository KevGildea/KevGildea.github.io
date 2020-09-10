---
title: "A novel deep learning based approach to characterising pedestrian pre-crash posture"
date: 2020-09-13
categories:
  - blog

tags:
  - Pedestrian safety
  - Integrated safety systems
  - Pose estimation
  - Shape estimation
  - Deep learning
  - Injury biomechanics
---

This is a review of a paper recently published in and presented at IRCOBI Europe 2020 (International Research Council on Injury Biomechanics). The study involves applying deep learning approaches to the task of classifying pedestrian pre-crash pose. This paper is exciting for a number of reasons; primarily due to the fact that this is the first published attempt to use pose and shape estimation in the field of traumatic injury biomechanics, but also the tailored approach they use with existing pose/shape estimation method to achieve more accurate predictions for the task.

>['Extracting Quantitative Descriptions of Pedestrian Pre-crash Postures from Real-world Accident
Videos
, M. Schachner et al. (2020)'](http://www.ircobi.org/wordpress/downloads/irc20/pdf-files/37.pdf)

Firstly for some context, let me tell you a little about the background of vehicle safety systems. They can be classified as being 'active', 'passive', or a combination of the two. Active safety systems are onboard electronic devices that are continuously 'active' and monitoring to avoid collision occurence, e.g. traction control, automatic emergency braking, blind spot detection. Whereas, passive safety systems are design features or devices that are generally inactive, only taking effect upon collision occurence to reduce injury outcomes, e.g. helmets, seat belts, air bags, vehicle/infrastructural design (softer/energy dissapating impact surfaces). Integrated safety systems are a combination of the two, where there is an elmement of continuous monitoring with informs the deployment of a passive safety system, e.g. advanced airbag deployment systems.

Pedestrian safety in vehcicle collisions is assesed by regulated type-testing, or by consumer organisations with more comprehensive testing protocols for passive and active safety systems (e.g. EuroNCAP). These tests include assesments of the effects of vehicle front geometry on injury outcomes, and the effectiveness of autonomous emergency braking or evasive steering assistant systems. Vehicle type-testing protocols for both active and passive safety systems currently use a simplified poses and motions exemplifying an unaware pedestrian walking in front of the vehicle with no consideration of reactions.

<p align="center">
  <img src="/assets/images/Ped-Passive.PNG" width="500">
</p>

<p align="center">
  <img src="/assets/images/Ped-AEB.gif" width="500">
</p>


However, it is known that pedestrians exhibit certain reactionary postures and motions before being impacted by a car, as described in this paper and other published literature [[1](https://pubmed.ncbi.nlm.nih.gov/24435730/), [2](http://www.ircobi.org/wordpress/downloads/irc17/pdf-files/26.pdf)].

| Jump            |  Attempt to avoid |  Freeze in place |
:-------------------------:|:-------------------------:|:-------------------------:
![](/assets/images/Ped-Pose-Jump.png)  |  ![](/assets/images/Ped-Pose-Avoid.png)  |  ![](/assets/images/Ped-Pose-Freeze.png)

#### Methodology

The value of this study lies in its adaptations to an existing shape estimation method called SMPLify [[3](http://files.is.tue.mpg.de/black/papers/BogoECCV2016.pdf)] to create a toolchain. SMPLify is an optimization approach that allows for 3D body pose and shape estimates to be made from a single input image with 2D pose estimates as input. 

![](/assets/images/Ped-Pose-Pred.png)

As context, SMPLify fits the a statistical human body model called SMPL [[4](http://files.is.tue.mpg.de/black/papers/SMPL2015.pdf)] to an image with DeepCut 2D pose estimates as input [[5](https://pose.mpi-inf.mpg.de/contents/pishchulin16cvpr.pdf)]. It achieves this by employing an optimization procedure with an objective function containing five error terms. The current study effectively uses SMPLify, with six adaptations to improve pose and shape estimation results for pedestrian pre-crash posture:

1) The 2D pose estimates are inferred using Openpose [[6](https://arxiv.org/abs/1812.08008)], which outperforms DeepCut. 
2) 2D estimates are manually improved on visual inspection.

<p align="center">
  <img src="/assets/images/Openpose-Manual-Annotation.PNG" width="500">
</p>

3) 4) & 5) Three adaptations are made to the SMPLify optimization procedure: 
   - the shape coefficients  are optimised globally over all images in a sequence leading up to the impact.
   - temporal information has been included an error term to be minimized i.e. the sum of joint distances across adjacent frames.
   - the interpenetration term (Pose prior 3) is replaced with a more recent approach which uses rays to detect self-intersection of outer surfaces of the mesh [[7](https://arxiv.org/abs/1901.08274)].

![](/assets/images/SMPLifyAdaptations.png)

6) SMPL joints do not represent the human skeleton , i.e., the joint locations are estimated based on a regressor that predicts the location of the joints as a function of the body shape [[4](http://files.is.tue.mpg.de/black/papers/SMPL2015.pdf)]. For this reason the joint system used in the optimization procedure were defined to best approximate the recommendations of the International Society of Biomechanics (ISB) [[8](https://www.sciencedirect.com/science/article/abs/pii/S0021929001002226), [9](https://www.sciencedirect.com/science/article/abs/pii/S002192900400301X)].

<p align="center">
  <img src="/assets/images/SMPLjoints.PNG" width="400">
</p>

<p align="center">
  <img src="/assets/images/ISBApproximations.PNG" width="500">
</p>

7) Since the pose prior terms of the optimization procedure penalize unnatural human poses, and interpenetrations, which are likely to occur when they impacted, the results may be conservative for frames in the impact phase i.e. predict less realistic poses in the impact phase. For this reason the weighting factors for pose and shape terms in the optimization were relaxed in the final iterations of the optimization procedure, in effect allowing for less natural poses.

The optimization weights were determined using a commonly used and publicly available motion capture dataset, i.e., Human3.6M [[10](http://vision.imar.ro/human3.6m/description.php)]. 

<p align="center">
  <img src="/assets/images/h36mVsSMPL.png" width="400">
</p>

MPJPE or 'Mean Per Joint Position Error' is the most commonly used metric for bencmark tests in 3D human pose estimation, i.e. the mean of per joint position error (euclidian distance from ground truth) for all joints.

<p align="center">
  <img src="/assets/images/MPJPE.png" width="350">
</p>


Overcoming problems associated with MPJPE (use of joint angles)


#### Discussion

This method improves on all previous attempts to quantitatively characterise pre-impact pedestrian pose, which relied on either volunteer test in simulated environments [[1](https://pubmed.ncbi.nlm.nih.gov/24435730/)], or  visual inspection of crash footage [[2](http://www.ircobi.org/wordpress/downloads/irc17/pdf-files/26.pdf)]. Approaches like this may help guide changes to the boundary conditions of vehicle safety assesment tests, i.e., provide more representative postures for vehicle type-testing. Though the system is not automatic and requires some manual annotation, this may be a step towards a fully automated toolchain. This technique may also be a first step towards integrated pedestrian safety systems e.g. pose dependent bonnet deployment systems.

ADD EXAMPLES

More generally, this study demonstrates the importance of task specific approaches, i.e. making adaptations to existing deep learning techniques before applying them to defined tasks.

ADD INFO ON POSSIBLE IMPROVEMENTS AND FUTURE DIRECTIONS
i.e. add context information for VIBE (SMPL - SMPLify - SPIN - VIBE & AMASS - STAR - Graph-CMR) to the DL-MoCap post. Mention that improvements and a more automatic procedure may be achieved using SPIN or VIBE (which may be further improved using STAR in place of SMPL). Mention that the SOTA changes so rapidly (twice or 3 times since this paper was submitted).

h36m dataset only contains natural poses?



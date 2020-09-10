---
title: "A novel deep learning based approach to determining pedestrian pre-crash posture"
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

As context, SMPLify fits the a statistical human body model called SMPL [[4](http://files.is.tue.mpg.de/black/papers/SMPL2015.pdf)] to an image with DeepCut 2D pose estimates as input [[5](https://pose.mpi-inf.mpg.de/contents/pishchulin16cvpr.pdf)]. It achieves this by employing an optimization proceedure with an objective function containing five error terms. The current study effectively uses SMPLify, with five adaptations to improve pose and shape estimation results for pedestrian pre-crash posture:
1. the 2D pose estimates are inferred using Openpose [[6](https://arxiv.org/abs/1812.08008)], which outperforms DeepCut. 
2. 2D estimates are manually improved on visual inspection.
3. three adaptations are made to the SMPLify optimization procedure: 
   - the shape coefficients  are optimised globally over all images in a sequence leading up to the impact.
   - temporal information has been included an error term to be minimized i.e. the sum of joint distances across adjacent frames.
   - the interpenetration term (Pose prior 3) is replaced with a more recent approach which uses rays to detect self-intersection of outer surfaces of the mesh [[1](https://arxiv.org/abs/1901.08274)].

![](/assets/images/SMPLifyAdaptations.png)

ADD JOINT CONVENTIONS INFO HERE

Overcoming problems associated with MPJPE (use of joint angles)


#### Discussion

This method improves on all previous attempts in quantitatively characterising pre-impact pedestrian pose, which relied on visual inspections of crash footage [[1](https://pubmed.ncbi.nlm.nih.gov/24435730/), [2](http://www.ircobi.org/wordpress/downloads/irc17/pdf-files/26.pdf)], and may be a step towards a fully automated toolchain. Studies like this may help guide changes to the boundary conditions of vehicle safety assesment tests, i.e., provide more representative postures for vehicle type-testing. Though the system is not automatic and requires some manual annotation, this technique may be a valuable first step towards an integrated pedestrian safety system involving tailored bonnet deployment systems (GIVE EXAMPLES AND GIFS)

This study demonstrates the importance of adaptations on deep learning approached in task specific approaches.

ADD INFOR ON POSSIBLE IMPROVEMENTS AND FUTURE DIRECTIONS
Add context information for VIBE (SMPL - SMPLify - SPIN - VIBE & AMASS - STAR - Graph-CMR) to the DL-MoCap post. Mention that improvements and a more automatic proceedure may be achieved using SPIN or VIBE (which may be further improved using STAR in place of SMPL). Mention that the SOTA changes so rapidly (twice or 3 times since this paper was submitted).



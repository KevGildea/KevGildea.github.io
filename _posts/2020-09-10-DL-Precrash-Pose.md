---
title: "A novel deep learning based approach to characterising pedestrian pre-crash posture"
date: 2020-09-10
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

This is a review of a paper recently published in and presented at IRCOBI Europe 2020 (International Research Council on Injury Biomechanics). The study involves applying deep learning approaches to the task of classifying pedestrian pre-crash pose. This paper is interesting for a number of reasons; primarily due to the fact that this is the first published attempt to use pose and shape estimation in the field of traumatic injury biomechanics, but also because of the adaptations the authors make to existing pose/shape estimation methods in order to achieve more accurate predictions for the task.

>['Extracting Quantitative Descriptions of Pedestrian Pre-crash Postures from Real-world Accident
Videos, Schachner et al. (2020)'](http://www.ircobi.org/wordpress/downloads/irc20/pdf-files/37.pdf)

Firsty I'll provide a little background information on vehicle safety systems. They can be classified as being 'active', 'passive', or a combination of the two. Active safety systems are onboard electronic devices that are continuously 'active' and monitoring to avoid collision occurence, e.g. traction control, automatic emergency braking, blind spot detection. Whereas, passive safety systems are design features or devices that are generally inactive, only taking effect upon collision occurence to reduce injury outcomes, e.g. helmets, seat belts, air bags, vehicle/infrastructural design (softer/energy dissapating impact surfaces). Integrated safety systems are a combination of the two, where there is an element of continuous monitoring which informs the deployment of a passive safety system, e.g. advanced airbag deployment systems.

Passive and active pedestrian safety systems are assesed through regulated vehicle type-testing, and by consumer organisations with more comprehensive testing protocols (e.g. EuroNCAP). These tests include assesments of the effects of vehicle front geometry on injury outcomes, and the effectiveness of autonomous emergency braking or evasive steering assistant systems. Current protocols for both active and passive safety systems use simplified pedestrian poses and motions exemplifying an unaware pedestrian walking in front of a vehicle, with no consideration of pedestrian reaction.

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

The value of this study lies in its adaptations to an existing pose/shape estimation method called SMPLify [[3](http://files.is.tue.mpg.de/black/papers/BogoECCV2016.pdf)] to create a toolchain. 

![](/assets/images/Ped-Pose-Pred.png)

For context, SMPLify fits a statistical human body model called SMPL [[4](http://files.is.tue.mpg.de/black/papers/SMPL2015.pdf)] to an image with DeepCut 2D pose estimates as input [[5](https://pose.mpi-inf.mpg.de/contents/pishchulin16cvpr.pdf)]. It does this by using an optimization procedure with an objective function containing five error terms. The current study uses SMPLify, with six adaptations to improve pose and shape estimation results for pedestrian pre-crash posture:

1) The 2D pose estimates are inferred using Openpose [[6](https://arxiv.org/abs/1812.08008)], which outperforms DeepCut. 

2) 2D estimates are manually improved on visual inspection.

<p align="center">
  <img src="/assets/images/Openpose-Manual-Annotation.PNG" width="500">
</p>

3) 4) & 5) Three adaptations are made to the SMPLify optimization procedure: 
   - The shape coefficients (*β*) are optimised globally over all images in a sequence leading up to the impact.
   - Temporal information has been included an error term to be minimized (*E<sub>fr</sub>*) i.e. the sum of joint distances across adjacent frames.
   - The interpenetration term (*E<sub>sp</sub>*) is replaced with a more recent approach which uses rays to detect self-intersection of outer surfaces of the mesh [[7](https://arxiv.org/abs/1901.08274)].

![](/assets/images/SMPLifyAdaptations.png)

6) Since the pose prior terms of the optimization procedure penalize unnatural human poses, and mesh interpenetrations, which are likely to occur when a pedestrian is impacted by a car, the results may be conservative for frames in the impact phase i.e. predict less realistic poses. For this reason the weighting factors for the pose and shape terms were relaxed in the final 100 (out of 1000) iterations of the optimization procedure, effectively allowing for less natural poses upon impact.

<p align="center">
  <img src="/assets/images/Ped-Pose-Config.PNG" width="500">
</p>


The optimization weights were determined using a commonly used and publicly available motion capture dataset, i.e., Human3.6M [[8](http://vision.imar.ro/human3.6m/description.php)]. 

<p align="center">
  <img src="/assets/images/h36mVsSMPL.png" width="400">
</p>

MPJPE or 'Mean Per Joint Position Error' is the most commonly used metric for benchmark tests in 3D human pose estimation, i.e. the mean of per joint position error (euclidian distance from ground truth) for all joints.

<p align="center">
  <img src="/assets/images/MPJPE.png" width="350">
</p>

However, the authors claim that the this metric has limitations, and that in some cases there can be low errors for incomparible poses, i.e., some obviously different poses can have misleadingly low values of MPJPE. So, the authors also investigate elbow and knee angles. Configuration 1 above was selected as having the best overall performance in testing.

SMPL joints do not represent the human skeleton, i.e., the joint locations are estimated based on a regressor that predicts the location of the joints as a function of the body shape [[4](http://files.is.tue.mpg.de/black/papers/SMPL2015.pdf)]. For this reason the joint system was revised to best approximate the recommendations of the International Society of Biomechanics (ISB) [[9](https://www.sciencedirect.com/science/article/abs/pii/S0021929001002226), [10](https://www.sciencedirect.com/science/article/abs/pii/S002192900400301X)].

<p align="center">
  <img src="/assets/images/SMPLjoints.PNG" width="400">
</p>

<p align="center">
  <img src="/assets/images/ISBApproximations.PNG" width="500">
</p>



#### Discussion

This method improves on all previous attempts to quantitatively characterise pre-impact pedestrian pose, which relied on either volunteer test in simulated environments [[1](https://pubmed.ncbi.nlm.nih.gov/24435730/)], or  visual inspection of crash footage [[2](http://www.ircobi.org/wordpress/downloads/irc17/pdf-files/26.pdf)]. This method also  overcomes a task specific issue for traumatic injury biomechanics relating to the penalisation of unnatural poses. Approaches like this may help guide changes to the boundary conditions of vehicle safety assesment tests, i.e., provide more representative postures for vehicle type-testing. Though the system is not automatic and requires some manual annotation, this may be a step towards a fully automated toolchain. This technique may also be a first step towards integrated pedestrian safety systems e.g. pose dependent bonnet deployment/active hood systems, or external airbag systems.

<p align="center">
  <img src="/assets/images/ActiveHood.gif" width="500">
</p>

3D pose and shape estimation is a rapidly evolving field, and since the submission of this paper, state-of-the-art methods in the area have changed multiple times. Though unlikely to significantly alter the effectiveness of a technique such as this, there is now a new state-of-the-art statistical human body shape model (STAR) [[11](https://arxiv.org/pdf/2008.08535.pdf)], which is intended as a replacement for SMPL. There have also been a couple of changes in state-of-the-art for pose and shape estimation, both of which have included the optimization procedure into the 2D pose estimator's deep neural network, i.e. SPIN (SMPL oPtimization IN the loop) [[13](https://arxiv.org/pdf/1909.12828.pdf)], and VIBE (Video Inference for Human Body Pose and Shape Estimation) [[14](https://arxiv.org/pdf/1912.05656.pdf)]. Similar to this study by Schachner et al. (2020), VIBE includes a temporal aspect which improves their predictions. It is reasonable to speculate that a similar approach with the optimization procedure included 'in the loop' along with the 2D pose estimator may achieve more accurate and automatic results for pedestrian pre-crash pose. 

More generally, this study demonstrates the importance of task specific approaches, i.e. making adaptations to existing deep learning techniques when applying them to defined tasks. The study also highlights the difficulties in obtaining sufficient quality in-the-wild footage, due to occlusions, low lighting conditions, low spatial resolution (image/video quality), or low temporal resolution (framerate).






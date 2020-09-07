---
title: "Deep learning techniques for human motion capture: an injury biomechanics perspective"
date: 2020-09-06
categories:
  - blog

tags:
  - Motion capture
  - Deep learning
  - Injury biomechanics
  - Multibody Dynamics
---


Motion capture is the process of recording human motion, it can be used for a variety of applications including character animation, and interactive gaming in the entertainment industry, robotic motion control and planning, or biomechanical applications such as injury and performance analysis. Since the late 1900s motion capture has been used for planar (2D) biomechanical kinematic analysis, i.e. the Rotoscope [[1](https://www.loc.gov/item/79051299/)]. Since then, a wide variety of 3D motion capture systems have been developed which allow for more detailed analysis. These can generally be divided into the categories of:
1. marker-based systems.
2. wearable sensor-based systems.
3. markerless systems.

This post is focused on the recent emergence of markerless deep learning approaches, for context, and since the accuracy assessment of many of these modern approaches rely on comparisons to traditional methods, a brief introduction to marker-based, sensor-based, and markerless systems is also presented. Though body and joint positional accuracy are important considerations in all applications of motion capture, they are of notable importance for human biomechanical analysis e.g. traumatic injury biomechanics, or physiotherapy. For this reason, this review focuses on the current and potential uses of motion capture in the field of traumatic injury biomechanics. Notwithstanding the significant developments in this area driven by the aim of improving motion realism in the entertainment industry.

The operating principles of motion capture generally involve: 
1. the tracking of human body keypoints which correspond to anatomical joint positions
2. inference of tracked keypoint locations to body kinematics by use of a defined kinematic chain i.e. a hierarchical chain of links and joints. 

These kinematic chains often involve the use of physically constrained joints, i.e. joints with less than 6 degrees of freedom (DOF). By taking estimates for link inertial properties i.e. body segment mass distributions, and creating a multibody system and applying inverse dynamics, the captured motion can be used to calculate dynamic information. Internal muscle response is also an important consideration and is an active research area for applications such as gait analysis, and traumatic impacts [[2](https://pubmed.ncbi.nlm.nih.gov/24950131/)]. Without consideration of the internal muscular forces and torques exerted during human motion, impact loads can be estimated; this approach is commonly referred to as ragdoll physics in the animation industry, and is commonly used in biomechanical applications which do not involve a significant amount of human controlled motion, e.g. road traffic collisions (RTCs) [[3](https://www.springer.com/gp/book/9789048127429)], or sports scenarios involving impact to an unaware player [[4](https://journals.sagepub.com/doi/10.1177/1747954119833477)]. Injury metrics have been developed which allow predictions of injury severity by body region based on their kinematic/dynamic response in collisions [[5](https://www.springer.com/gp/book/9783030116583)]. Most injury criteria are based on accelerations, relative velocities or displacements, or joint constraint forces, and need some mathematical evaluation of a time history signal. For inverse dynamics calculations, the accuracy of kinematic measurement is an important first step in biomechanical applications, as errors in joint position estimates propagate; resulting in even larger errors in dynamic estimates. Deep learning approaches applied to in-the-wild videos may allow for a more detialed understanding of human pose, and impact kinematics/dynamics, e.g. [[6](http://www.ircobi.org/wordpress/downloads/irc20/pdf-files/37.pdf)]. 

![image](/assets/images/mocapskeleton.png)

#### Traditional motion capture methods
Optical or optoelectronic motion capture systems, such as Vicon [[7](https://www.vicon.com/)], OptiTrack [[8](https://optitrack.com/)], Motion Analysis [[9](https://www.motionanalysis.com/)], and Qualisys [[10](https://www.qualisys.com/)] involve the tracking of passive retroreflective markers placed on a human subject, using multiple calibrated high-framerate cameras (>200fps) with light emitters (usually infrared). Active marker-based systems also exist, which use LED markers in place of passive retroreflective markers, eliminating the need for light emitters [[11](https://www.ndigital.com/msci/products/optotrak-certus/)]. These systems obtain 3D positional cartesian coordinates, i.e. 3 degrees of freedom (3DOFs) for each marker by time of flight and geometric triangulation. Vicon is the most widely used passive marker-based system and is used as a proprietary eponym. Underlying skeletal joint positions and orientations (6DOFs) can be automatically estimated by inference from external markers [[12](https://docs.vicon.com/display/Nexus210/About+labeling+skeleton+templates)]. Joint positions are calculated using groups of markers that move in the same way, with a minimum of 3 markers needed per joint to infer 6DOFs. These joints are positioned to approximate the human skeletal structure, and their kinematic nature with differing degrees of freedom (Free Joint: 6DOF, Ball Joint: 3DOFs, Hardy Spicer Joint: 2DOFs, Hinge Joint: 1DOF) limit the axes that the links are free to rotate about; effectively reducing unrealistic motions [[13](https://docs.vicon.com/display/Nexus210/Link+segments)]. Custom kinematic skeleton formats may also be created [[14](https://docs.vicon.com/display/Nexus210/Create+a+labeling+skeleton+template)]. Some marker-based systems have additional biomechanical analysis features; for example, Vicon has a plugin gait feature for calculation of lower and upper body dynamics such as joint forces, moments, and powers [[15](https://docs.vicon.com/display/Nexus210/Lower+body+modeling+with+Plug-in+Gait#LowerbodymodelingwithPluginGait-OutputsLowerBody)], [[16](https://docs.vicon.com/display/Nexus210/Full+body+modeling+with+Plug-in+Gait)]. 

![image](/assets/images/vicon.gif)

There are also a variety of alternative motion capture systems that involve markers/sensors, including: 
- inertial systems involving the use of inertial measurement units (i.e. combined gyroscope(s), and accelerometer(s)) [[17](https://www.xsens.com/)], [[18](https://www.motusglobal.com/mx-platform)]. 
- mechanical systems involving the use of an instrumented exoskeleton (with sliders and potentiometers) [[19](https://www.repository.cam.ac.uk/handle/1810/256141)]. 
- magnetic systems involving both magnetic sensor markers and a magnetic field generator [[20](https://ieeexplore.ieee.org/document/908928)].

Though the accuracy of many of these marker/sensor-based systems are high; they are prohibitively expensive for many, and the experimental setups are unsuitable for many in-the-wild biomechanical applications. Markerless motion capture systems allow for more natural subject motion and aim for capture in less experimentally constrained environments (i.e. outside of a motion capture laboratory) [[21](https://www.cs.cmu.edu/~hanbyulj/panoptic-studio/), [22](http://www.thecaptury.com/), [23](https://tracklab.com.au/organic-motion/), [24](http://www.simi.com/en/)]. The first human motion capture system to be used for biomechanical analysis, the Rotoscope, invented by Max Fleisher in 1919, was in fact a markerless system. The system involves manual tracing of character outlines for individual frames of an image sequence. Most famously, this system was used by to investigate human and equine gait [[1](https://www.loc.gov/item/79051299/)]. 

![image](/assets/images/rotoscope.png)

More recent computer-based methods now exist which employ spatially calibrated multi camera setups; streamlining the process and allowing for 3D analysis to be performed. These systems may be automatic e.g. [[21](https://www.cs.cmu.edu/~hanbyulj/panoptic-studio/), [24](http://www.simi.com/en/)] or require manual annotation [[25](https://www.posersoftware.com/)]. Systems involving both colour and depth maps (i.e. RGB-D cameras) such as the Microsoft Kinect has potential to allow for accurate single-camera motion capture, though the accuracy of the Kinect V2 is currently inadequate for many biomechanical applications. There have been efforts to improve upon the accuracy of the Kinect's skeletal tracking capabilities, all in some way involve optimizing certain parameters to achieve more realistic motions. The most successful (using 3 Kinect V1s) involved a physics-based approach utilizing body segment mass estimates from the Kinect depth sensors, insole pressure sensors, and optimization of the equations of motion [[26](https://dl.acm.org/doi/10.1145/2661229.2661286)]. Another approach that achieved a similar, albeit slightly lower level of accuracy involved imposing ellipsoids on body segments based on a mesh and minimizing cross over between them, and joint rotation angle boundaries (using 2x Kinect v2s) [[27](https://ieeexplore.ieee.org/document/7390092)]. This approach did not involve the equations of motion and did not require the use of any wearable sensors. However, the requirement of multiple RGB-D sensors makes a system such as this unsuitable for in-the-wild biomechanics applications. Comercially available softwares also exist which allow for the use of multiple fused depth sensors in a relatively inexpensive and accurate motion capture setup [[28](http://ipisoft.com/)].

![image](/assets/images/ipisoft.gif)

One manual method used in the realm of biomechanical research called Multibody Image Matching (MBIM) has allowed for extraction of 3D pose from in-the-wild videos e.g. [[4](https://journals.sagepub.com/doi/10.1177/1747954119833477)]. 

![image](/assets/images/poser.PNG)

Though MBIM achieves high accuracy for certain applications [[28](https://pubmed.ncbi.nlm.nih.gov/28632058/)], it is labor-intensive and are unsuitable for real-time applications. Furthermore, currently available automatic markerless systems involve a large number of calibrated cameras in controlled lab-based settings.

#### Machine learning approaches
For (near) real-time and in-the-wild applications there is a need for automatic 3D tracking of joint positions using simple inexpensive cameras. Deep learning has recently been applied in this area with great success. These approaches have allowed for robust and fast (multi) human pose estimation outside of laboratory conditions. Generally, these systems involve the training of a model with prior ground truth data. Pose estimation approaches can be categorized as: 
1. bottom-up approaches, which first find the keypoints and then maps them to different people in the image. 
2. top-down approaches, which use a mechanism to detect people in an image, apply a bounding box around each person, and then estimate keypoint configurations within the bounding boxes. 

Many deep learning approaches to 2D pose estimation have been developed [[30](https://arxiv.org/abs/1812.08008), [31](https://arxiv.org/abs/1312.4659), [32](https://arxiv.org/abs/1612.00137), [33](https://arxiv.org/abs/1902.09212)]. Due to its accuracy and robustness, Openpose is widely considered to be the state-of-the-art method for 2D multi-person pose estimation [[29](https://arxiv.org/abs/1812.08008)]. Openpose is a bottom-up approach that uses Part Affinity Fields (PAFs), to learn to associate body parts with individuals in images.

![image](/assets/images/openpose-kevin.gif)

However, a more recent approach HRNet outperforms Openpose slightly by retaining a high-resolution image representation throughout the training process [[31](https://arxiv.org/abs/1312.4659)]. 

3D pose estimation methods generally employ a 2D pose estimator as a backbone, and use techniques to project these into the 3D realm. For multi-camera setups, a simple approach involves geometric triangulation, i.e. exploiting the knowledge of camera intrinsic and extrinsic parameters of a camera to triangulate 2 or more views of a keypoint into 3D space [[34](https://www.cambridge.org/core/books/multiple-view-geometry-in-computer-vision/0B6F289C78B2B23F596CAA76D3D43F7A)]; in fact, Openpose contains a module for this [[35](https://github.com/CMU-Perceptual-Computing-Lab/openpose#3-d-reconstruction-module-body-foot-face-and-hands)]. 

![image](/assets/images/openpose3d.gif)

A promising approach which does not require pre-defined calibration parameters, learnable triangulation, includes this geometric triangulation into the architecture [[36](https://arxiv.org/abs/1905.05754)]. 

3D single-camera approaches have also been developed e.g. [[37](https://arxiv.org/abs/1912.05656), [38](https://arxiv.org/abs/1903.02330), [39](https://arxiv.org/abs/2003.14179)]. GAST-Net (Graph Attention Spatio-Temporal convolutional Network) is the state-of-the-art method, and addresses problems experienced around occlusion and depth ambiguities in previous methods by including spatiotemporal information (i.e. learning kinematic constraints such as posture, 2nd order joint relations, and symmetry) [[40](https://arxiv.org/abs/2003.14179)]. GAST-Net has achieved accuracy within 2.2cm of marker-based motion capture methods, and outperforms previous methods particularly in cases involving heavy self-occlusion and fast motion.

![image](/assets/images/gastnet-kevin.gif)

3D pose and shape estimation methods also exist, which allow for the inclusion of body shape predictions. Combined body pose and shape estimation is useful from an injury biomechanics perspective; with both kinematics (pose) and estimates for body segment inertia tensors (inferred from the body shape estimate) inverse dynamics can be performed, which may allow for more detailed injury predictions. The most promising approaches involve the use of a statistical human body shape model (e.g. SMPL [[41](http://files.is.tue.mpg.de/black/papers/SMPL2015.pdf)], GraphCMR [[42](https://arxiv.org/pdf/1905.03244.pdf)], SPIN [[43](https://arxiv.org/pdf/1909.12828.pdf)], STAR (state-of-the-art) [[44](https://arxiv.org/abs/2008.08535)]), i.e. a skinned vertex-based model that accurately represents a wide variety of body shapes in natural human poses, developed via dimensionality reduction techniques i.e. Principal Component Analysis (PCA). 

![image](/assets/images/GT-SMPL-STAR.PNG)

The current state-of the art 3D pose and shape estimation method VIBE [[45](https://arxiv.org/abs/1912.05656)] estimates SMPL body model parameters for each frame in a video sequence using a temporal generation network, which is trained together with a motion discriminator i.e. AMASS [[46](http://files.is.tue.mpg.de/black/papers/amass.pdf)].

![image](/assets/images/vibe-kevin.gif)



#### Conclusions and future directions
The trajectory of advancement in deep learning motion capture methods has mirrored that of traditional ones. Early iterations of deep learning-based motion capture have focused on planar joint position estimates from monocular viewpoints. These systems have achieved remarkable accuracy, and consequently, more recent efforts have been pushing towards the 3D realm. The accuracy of these systems are currently below that of gold standard systems, or other markerless systems involving depth sensors or multi-camera setups, however, this is an emerging research topic, and with the transformative effects deep learning approaches have had in other fields in the near future we can expect to see rapid improvements.

##### Sources to monitor for developments:

- [Github](https://github.com/topics/3d-pose-estimation)
- [Papers with code](https://paperswithcode.com/task/3d-human-pose-estimation)







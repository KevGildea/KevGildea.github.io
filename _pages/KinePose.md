---
permalink: /KinePose/
title: "KinePose: A temporally optimised inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints"
---

<p align="center">
  <img src="/assets/images/KinePose/KinePose2.png" width="900">
</p>

## Introduction
KinePose is an innovative approach for 6 Degrees of Freedom (DOF) human pose estimation, incorporating Inverse Kinematics (IK) with biomechanical constraints. Developed for diverse applications ranging from sports to impact analysis, KinePose offers enhanced biomechanical relevance in monocular human pose estimation.

<p align="center">
  <img src="/assets/images/KinePose/KinePose_pipeline_3.png" width="400">
</p>


## Tools

### For use with the suite of ellipsoid human body models in MADYMO (MAthematical DYnamic MOdels)

<p align="center">
  <img src="/assets/images/KinePose/MADYMO-KinePose.jpg" width="250">
</p>

| Step                  | Description                                                  | Tools                                     | Manuals                                  |
|-----------------------|--------------------------------------------------------------|-------------------------------------------|------------------------------------------|
| 2D Pose               | Initial pose estimation in pixel coordinates. Options: <br> 1) fully automatic (YOLOv8), <br> 2) semi-automatic with manual refinement, <br> 3) fully manual. | [Tools](https://drive.google.com/file/d/17kg8gPE_3GLgzm0N8T30WZ-OGaaxGW5b/view?usp=sharing){:target="_blank"} | TBD |
| 3D Pose               | Lifting from 2D to 3D pose (MotionBERT).                       | [Tool](https://drive.google.com/file/d/1FNhjppB2Ct-3V9M_CYxV5xXChSUIXVcI/view?usp=sharing){:target="_blank"} | TBD |
| 6DOF Pose             | IK optimisation to a 6DOF pose (KinePose).                   | [Tool](https://drive.google.com/file/d/12kGWue4mzFBMf21Ud6nYXUxYg7tRIGRZ/view?usp=sharing){:target="_blank"} | TBD |


### For use with SMPL/SMPL-X

Work in progress...

<p align="center">
  <img src="/assets/images/KinePose/SMPLX.PNG" width="350">
</p>

### For use with the PIPER HBM

Work in progress...

<p align="center">
  <img src="/assets/images/KinePose/PIPERCHILD.png" width="100">
</p>

### For use with VIVA+ HBMs

TBD

[comment]: <> (https://www-esv.nhtsa.dot.gov/Proceedings/27/27ESV-000242.pdf)

### For use with the OpenSim HBM

TBD

[comment]: <> ()

### General-purpose (user customisable biomechanical model)

TBD


## Example applications

1) Baseball swing analysis


<p align="center">
  <img src="/assets/images/KinePose/Baseball.gif" width="500">
</p>


2) Single bicycle crash reconstruction


<p align="center">
  <img src="/assets/images/KinePose/SBC.gif" width="500">
</p>


3) Reconstruction of representative pedestrian pre-impact poses


<p align="center">
  <img src="/assets/images/KinePose/Train.png" width="600">
</p>

4) Rugby tackling pose estimation and reconstruction


<p align="center">
  <img src="/assets/images/KinePose/Rugby.PNG" width="600">
</p>


## Conference presentations

- Congress of the European Society of Biomechanics (<a href="https://esbiomech.org/welcome-to-the-european-society-of-biomechanics-esbiomech/esb-related-publications/esb-congresses-abstracts/" target="_blank">ESB 2022</a>)
- Irish Machine Vision & Image Processing Conference (<a href="https://imvipconference.github.io/" target="_blank">IMVIP 2022</a>)

## Cite our methods papers
If you find KinePose useful in your research, please consider citing our work:

<small>
Gildea, K., Mercadal-Baudart, C., Blythman, R., Smolic, A., & Simms, C. (2022). KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints. In *Irish Machine Vision & Image Processing Conference (IMVIP)*. <a href="https://arxiv.org/pdf/2207.12841.pdf" target="_blank">10.56541/QTUV2945</a>  <a href="https://kevgildea.github.io/assets/docs/KinePose/SuppMat.pdf" target="_blank">SuppMat</a>
</small>


<small>
Gildea, K., Hall, D., Cherry, C., & Simms, C. (2024). Forward dynamics computational modelling of a cyclist fall with the inclusion of protective response using deep learning-based human pose estimation. *Journal of Biomechanics. <a href="https://doi.org/10.1016/j.jbiomech.2024.111959" target="_blank">10.1016/j.jbiomech.2024.111959</a>
</small>


<a href="/assets/images/KinePose/KinePose_Citation.bib" download>Download citation (.bib)</a>



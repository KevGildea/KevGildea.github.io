---
permalink: /KinePose/
title: "KinePose: A temporally optimised inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints"
---

<p align="center">
  <img src="/assets/images/KinePose/KinePose2.png" width="900">
</p>

## Introduction
KinePose is an innovative approach for 6 Degrees of Freedom (DOF) human pose estimation, incorporating Inverse Kinematics (IK) with biomechanical constraints. Developed for diverse applications ranging from sports to impact analysis, KinePose offers enhanced biomechanical relevance in monocular human pose estimation.

## Tools

### For use with the suite of ellipsoid human body models in MADYMO (MAthematical DYnamic MOdels)

| Step                  | Description                                                  | Tools                                     | Manuals                                  |
|-----------------------|--------------------------------------------------------------|-------------------------------------------|------------------------------------------|
| 2D Pose               | Initial pose estimation in pixel coordinates. <br> 1) fully automatic (YOLOv8), <br> 2) semi-automatic with manual refinement, <br> 3) fully manual. | [Tools](https://drive.google.com/file/d/17kg8gPE_3GLgzm0N8T30WZ-OGaaxGW5b/view?usp=sharing){:target="_blank"} | TBD |
| 3D Pose               | Lifting from 2D to 3D pose.                       | TBD | TBD |
| 6DOF Pose             | IK optimisation to a 6DOF pose (KinePose).                   | [Tool](https://drive.google.com/file/d/12kGWue4mzFBMf21Ud6nYXUxYg7tRIGRZ/view?usp=sharing){:target="_blank"} | TBD |



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
  <img src="/assets/images/KinePose/Train.png" width="500">
</p>

4) Rugby tackling pose estimation and reconstruction


<p align="center">
  <img src="/assets/images/KinePose/Rugby.PNG" width="900">
</p>


## Conference presentations
- [Congress of the European Society of Biomechanics (ESB 2022)](https://esbiomech.org/welcome-to-the-european-society-of-biomechanics-esbiomech/esb-related-publications/esb-congresses-abstracts/)
- [Irish Machine Vision & Image Processing Conference (IMVIP 2022)](https://imvipconference.github.io/)

## Cite our methods papers
If you find KinePose useful in your research, please consider citing our work:

```
@inproceedings{Gildea22,
    author    = {Gildea, Kevin and Mercadal-Baudart, Clara and Blythman, Richard and Smolic, Aljosa and Simms, Ciaran},
    title     = {KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints},
    booktitle = {Irish Machine Vision \& Image Processing Conference (IMVIP)},
    year      = {2022},
    doi       = {10.56541/QTUV2945}
}

@article{Gildea24,
    title     = {Forward dynamics computational modelling of a cyclist fall with the inclusion of protective response using deep learning-based human pose estimation},
    journal   = {Journal of Biomechanics},
    pages     = {111959},
    year      = {2024},
    issn      = {0021-9290},
    doi       = {https://doi.org/10.1016/j.jbiomech.2024.111959},
    author    = {Kevin Gildea and Daniel Hall and Christopher Cherry and Ciaran Simms}
}
```

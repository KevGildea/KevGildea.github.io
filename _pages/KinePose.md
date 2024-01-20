---
permalink: /KinePose/
title: "KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints (IMVIP)"
---

<p align="center">
  <img src="/assets/images/KinePose/KinePose2.png" width="900">
</p>

<p style="text-align: center;">
<a href="http://arxiv.org/abs/2207.12841" target="_blank">arXiv</a> ︱ <a href="https://github.com/KevGildea/KinePose" target="_blank">Code</a> ︱ <a href="https://kevgildea.github.io/assets/docs/KinePose/SuppMat.pdf" target="_blank">SuppMat</a>
</p>  
   


**Abstract**
Computer vision/deep learning-based 3D human pose estimation methods aim to localize human joints from images and videos. Pose representation is normally limited to 3D joint positional/translational degrees of freedom (3DOFs), however, a further three rotational DOFs (6DOFs) are required for many potential biomechanical applications. Positional DOFs are insufficient to analytically solve for joint rotational DOFs in a 3D human skeletal model. Therefore, we propose a temporal inverse kinematics (IK) optimization technique to infer joint orientations throughout a biomechanically informed, and subject-specific kinematic chain. For this, we prescribe link directions from a position-based 3D pose estimate. Sequential least squares quadratic programming is used to solve a minimization problem that involves both frame-based pose terms, and a temporal term. The solution space is constrained using joint DOFs, and ranges of motion (ROMs). We generate 3D pose motion sequences to assess the IK approach both for general accuracy, and accuracy in boundary cases.
Our temporal algorithm achieves 6DOF pose estimates with low Mean Per Joint Angular Separation (MPJAS) errors (3.7&deg;/joint overall, &  1.6&deg;/joint for lower limbs). With frame-by-frame IK we obtain low errors in the case of bent elbows and knees, however, motion sequences with phases of extended/straight limbs results in ambiguity in twist angle. With temporal IK, we reduce ambiguity for these poses, resulting in lower average errors.


<p align="center">
  <img src="/assets/images/KinePose/Baseball.gif" width="900">
</p>



**Presented at:**

- Congress of the European Society of Biomechanics (<a href="https://esbiomech.org/welcome-to-the-european-society-of-biomechanics-esbiomech/esb-related-publications/esb-congresses-abstracts/" target="_blank">ESB 2022</a>)

- Irish Machine Vision & Image Processing Conference (<a href="https://imvipconference.github.io/" target="_blank">IMVIP 2022</a>)



**Cite:**

```
@inproceedings{Gildea22,
    author    = {Gildea, Kevin and Mercadal-Baudart, Clara and Blythman, Richard and Smolic, Aljosa and Simms, Ciaran},
    title     = {KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints},
    booktitle = {Irish Machine Vision \& Image Processing Conference (IMVIP)},
    year      = {2022},
    doi       = {10.56541/QTUV2945}
}

@article{Gildea24,
title = {Forward dynamics computational modelling of a cyclist fall with the inclusion of protective response using deep learning-based human pose estimation},
journal = {Journal of Biomechanics},
pages = {111959},
year = {2024},
issn = {0021-9290},
doi = {https://doi.org/10.1016/j.jbiomech.2024.111959},
author = {Kevin Gildea and Daniel Hall and Christopher Cherry and Ciaran Simms}
}
```


---
permalink: /KinePose/
title: "KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints (IMVIP 2022)"
---

<p align="center">
  <img src="/assets/images/KinePose/KinePose2.png" width="900">
</p>

<p style="text-align: center;">
<a href="https://arxiv.org/" target="_blank">Paper</a> ︱ <a href="https://github.com/KevGildea/KinePose" target="_blank">Code</a> ︱ <a href="https://kevgildea.github.io/assets/images/KinePose/SuppMat.pdf" target="_blank">SuppMat</a>
</p>
   


**Abstract**
Computer vision/deep learning-based 3D human pose estimation methods aim to localize human joints from images and videos. Pose representation is normally limited to 3D joint positional/translational degrees of freedom (3DOFs), however, a further three rotational DOFs (6DOFs) are required for many potential biomechanical applications. Positional DOFs are insufficient to analytically solve for joint rotational DOFs in a 3D human skeletal model. Therefore, we propose a temporal inverse kinematics (IK) optimization technique to infer joint orientations throughout a biomechanically informed, and subject-specific kinematic chain. For this, we prescribe link directions from a position-based 3D pose estimate. Sequential least squares quadratic programming is used to solve a minimization problem that involves both frame-based pose terms, and a temporal term. The solution space is constrained using joint DOFs, and ranges of motion (ROMs). We generate 3D pose motion sequences to assess the IK approach both for general accuracy, and accuracy in boundary cases.
Our temporal algorithm achieves 6DOF pose estimates with low Mean Per Joint Angular Separation (MPJAS) errors (3.7&deg;/joint overall, &  1.6&deg;/joint for lower limbs). With frame-by-frame IK we obtain low errors in the case of bent elbows and knees, however, motion sequences with phases of extended/straight limbs results in ambiguity in twist angle. With temporal IK, we reduce ambiguity for these poses, resulting in lower average errors.


<p align="center">
  <img src="/assets/images/KinePose/Baseball.gif" width="900">
</p>



**In proceedings:**

- Congress of the European Society of Biomechanics (<a href="https://esbiomech.org/welcome-to-the-european-society-of-biomechanics-esbiomech/esb-related-publications/esb-congresses-abstracts/" target="_blank">ESB 2022</a>)

- Irish Machine Vision & Image Processing Conference (<a href="https://imvipconference.github.io/" target="_blank">IMVIP 2022</a>)



**Cite:**

```
@inproceedings{Gildea22,
    author    = {Gildea, Kevin and Mercadal-Baudart, Clara and Blythman, Richard and Smolic, Aljosa and Simms, Ciaran},
    title     = {KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints},
    booktitle = {IMVIP},
    year      = {2022},
}
```


---
permalink: /KinePose/
title: "KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints"
---


## KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints (IMVIP 2022)

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


## Appeared in
- Congress of the European Society of Biomechanics (<a href="https://esbiomech.org/welcome-to-the-european-society-of-biomechanics-esbiomech/esb-related-publications/esb-congresses-abstracts/" target="_blank">ESB 2022</a>)

- Irish Machine Vision & Image Processing Conference (<a href="https://imvipconference.github.io/" target="_blank">IMVIP 2022</a>)


## Citation
```
@inproceedings{Gildea22,
    author    = {Gildea, Kevin and Mercadal-Baudart, Clara and Blythman, Richard and Smolic, Aljosa and Simms, Ciaran},
    title     = {KinePose: A temporally optimized inverse kinematics technique for 6DOF human pose estimation with biomechanical constraints},
    booktitle = {IMVIP},
    year      = {2022},
}
```


# OSSO: Obtaining Skeletal Shape from Outside (CVPR 2022)

This repository contains the official implementation of the skeleton inference from:

**OSSO: Obtaining Skeletal Shape from Outside** <br>*Marilyn Keller, Silvia Zuffi, Michael J. Black and Sergi Pujades* <br>[Full paper](https://download.is.tue.mpg.de/osso/OSSO.pdf) | [Project website](https://osso.is.tue.mpg.de/index.html#Dataset) 


Given a body shape with SMPL or STAR topology (in blue), we infer the underlying skeleton (in yellow).
![teaser](./figures/skeleton_results.png)


## Installation
Please follow the installation instruction in [installation.md](installation.md) to setup all the required packages and models.


## Run skeleton inference

The skeleton can be inferred either from a [SMPL](https://smpl.is.tue.mpg.de/) or [STAR](https://github.com/ahmedosman/STAR) mesh.

``` 
python main.py  --mesh_input data/demo/body_female.ply --gender female -D -v
```

The final infered skeleton will be saved in the `out` folder and the intermediate meshes in `out/tmp`.


## Citation

If you find this model & software useful in your research, please consider citing:

```
@inproceedings{Keller:CVPR:2022,
  title = {{OSSO}: Obtaining Skeletal Shape from Outside},
  author = {Keller, Marilyn and Zuffi, Silvia and Black, Michael J. and Pujades, Sergi},
  booktitle = {Proceedings IEEE/CVF Conf.~on Computer Vision and Pattern Recognition (CVPR)},
  month = jun,
  year = {2022},
  month_numeric = {6}}
```

## Acknowledgements

OSSO uses the [Stitched Puppet](https://stitch.is.tue.mpg.de/) by Silvia Zuffi and Michael J. Black, and the body model [STAR](https://github.com/ahmedosman/STAR) by Ahmed Osman et al. The model was applied on [AGORA](https://agora.is.tue.mpg.de/) (Priyanka Patel et al.) for demonstration.

This research has been conducted using the UK Biobank Resource under the Approved Project ID 51951. The authors thank the International Max Planck Research School for Intelligent Systems for supporting Marilyn Keller. Sergi Pujades’ work was funded by the ANR SEMBA project. We thank Anatoscope (www.anatoscope.com) for the initial skeleton mesh and useful discussions.

We also thank A. A. Osman for his helpful advice on body models, P. Patel for helping test OSSO on AGORA, T. McConnel, Y. Xiu, S. Tripathi and T. Yin for helping with the submission and release, and P. Ghosh, J. Tesch, A. Chandrasekaran, V. F. Abrevaya, S. Sanyal, O. Ben-Dov and P. Forte for fruitful discussions, advice and proofreading. 


## License

This code and model are available for non-commercial scientific research purposes as defined in the [LICENSE.txt](LICENSE.txt) file.


## Contact

For more questions, please contact osso@tue.mpg.de

For commercial licensing, please contact ps-licensing@tue.mpg.de

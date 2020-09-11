#### Hierarchical Kinematic Human Mesh Recovery

We consider the problem of estimating a parametric model
of 3D human mesh from a single image. While there has been substantial
recent progress in this area with direct regression of model parameters,
these methods only implicitly exploit the human body kinematic structure, leading to sub-optimal use of the model prior. In this work, we
address this gap by proposing a new technique for regression of human
parametric model that is explicitly informed by the known hierarchical
structure, including joint interdependencies of the model. This results in
a strong prior-informed design of the regressor architecture and an associated hierarchical optimization that is flexible to be used in conjunction
with the current standard frameworks for 3D human mesh recovery. We
demonstrate these aspects by means of extensive experiments on standard benchmark datasets, showing how our proposed new design outperforms several 
existing and popular methods, establishing new stateof-the-art results. By considering joint interdependencies, our method is
equipped to infer joints even under data corruptions, which we demonstrate by conducting experiments under varying degrees of occlusion.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123620749.pdf

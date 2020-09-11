#### Appearance Consensus Driven Self-Supervised Human Mesh Recovery

We present a self-supervised human mesh recovery framework
to infer human pose and shape from monocular images in the absence of
any paired supervision. Recent advances have shifted the interest towards
directly regressing parameters of a parametric human model by supervising them on large-scale datasets with 2D landmark annotations. This
limits the generalizability of such approaches to operate on images from
unlabeled wild environments. Acknowledging this we propose a novel
appearance consensus driven self-supervised objective. To effectively disentangle the foreground (FG) human we rely on image pairs depicting the
same person (consistent FG) in varied pose and background (BG) which
are obtained from unlabeled wild videos. The proposed FG appearance
consistency objective makes use of a novel, differentiable Color-recovery
module to obtain vertex colors without the need for any appearance network; via efficient realization of color-picking and reflectional symmetry.
We achieve state-of-the-art results on the standard model-based 3D pose
estimation benchmarks at comparable supervision levels. Furthermore,
the resulting colored mesh prediction opens up the usage of our framework for a variety of appearance-related tasks beyond the pose and shape
estimation, thus establishing our superior generalizability.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123460766.pdf

https://sites.google.com/view/ss-human-mesh

https://github.com/val-iisc/ss_human_mesh

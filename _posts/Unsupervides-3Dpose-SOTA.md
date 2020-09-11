#### Unsupervised Cross-Modal Alignment for Multi-Person 3D Pose Estimation

We present a deployment friendly, fast bottom-up framework
for multi-person 3D human pose estimation. We adopt a novel neural
representation of multi-person 3D pose which unifies the position of
person instances with their corresponding 3D pose representation. This is
realized by learning a generative pose embedding which not only ensures
plausible 3D pose predictions, but also eliminates the usual keypoint
grouping operation as employed in prior bottom-up approaches. Further,
we propose a practical deployment paradigm where paired 2D or 3D pose
annotations are unavailable. In the absence of any paired supervision, we
leverage a frozen network, as a teacher model, which is trained on an
auxiliary task of multi-person 2D pose estimation. We cast the learning as
a cross-modal alignment problem and propose training objectives to realize
a shared latent space between two diverse modalities. We aim to enhance
the model’s ability to perform beyond the limiting teacher network by
enriching the latent-to-3D pose mapping using artificially synthesized
multi-person 3D scene samples. Our approach not only generalizes to
in-the-wild images, but also yields a superior trade-off between speed
and performance, compared to prior top-down approaches. Our approach
also yields state-of-the-art multi-person 3D pose estimation performance
among the bottom-up approaches under consistent supervision levels.

http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123580035.pdf

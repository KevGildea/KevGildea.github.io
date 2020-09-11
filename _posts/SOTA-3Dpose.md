#### Motion Guided 3D Pose Estimation from Videos

We propose a new loss function, called motion loss, for supervising models for monocular 3D Human pose estimation from videos.
It works by comparing the motion pattern of the prediction against
ground truth key point trajectories. In computing motion loss, we introduce pairwise motion encoding, a simple yet effective representation
for keypoint motion. We design a new graph convolutional network architecture, U-shaped GCN (UGCN). It captures both short-term and
long-term motion information to fully leverage the supervision from the
motion loss. We experiment training UGCN with the motion loss on two
large scale benchmarks: Human3.6M and MPI-INF-3DHP. Our models
surpass other state-of-the-art models by a large margin. It also demonstrates strong capacity in producing smooth 3D sequences and recovering
keypoint motion.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123580749.pdf

http://wangjingbo.top/papers/ECCV2020-Video-Pose/MotionLossPage.html

https://github.com/open-mmlab/mmskeleton/tree/master

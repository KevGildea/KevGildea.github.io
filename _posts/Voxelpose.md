#### VoxelPose: Towards Multi-Camera 3D Human Pose Estimation in Wild Environment

We present VoxelPose to estimate 3D poses of multiple people from multiple camera views. In contrast to the previous efforts which
require to establish cross-view correspondence based on noisy and incomplete 2D pose estimates, VoxelPose directly operates in the 3D space
therefore avoids making incorrect decisions in each camera view. To
achieve this goal, features in all camera views are aggregated in the 3D
voxel space and fed into Cuboid Proposal Network (CPN) to localize all
people. Then we propose Pose Regression Network (PRN) to estimate
a detailed 3D pose for each proposal. The approach is robust to occlusion which occurs frequently in practice. Without bells and whistles, it
outperforms the previous methods on several public datasets.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123460188.pdf

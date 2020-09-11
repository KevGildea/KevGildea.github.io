#### Pose2Mesh: Graph Convolutional Network for 3D Human Pose and Mesh Recovery from a 2D Human Pose

Most of the recent deep learning-based 3D human pose and
mesh estimation methods regress the pose and shape parameters of human mesh models, such as SMPL and MANO, from an input image.
The first weakness of these methods is the overfitting to image appearance, due to the domain gap between the training data captured from
controlled settings such as a lab, and in-the-wild data in inference time.
The second weakness is that the estimation of the pose parameters is
quite challenging due to the representation issues of 3D rotations. To
overcome the above weaknesses, we propose Pose2Mesh, a novel graph
convolutional neural network (GraphCNN)-based system that estimates
the 3D coordinates of human mesh vertices directly from the 2D human pose. The 2D human pose as input provides essential human body
articulation information without image appearance. Also, the proposed
system avoids the representation issues, while fully exploiting the mesh
topology using GraphCNN in a coarse-to-fine manner. We show that our
Pose2Mesh significantly outperforms the previous 3D human pose and
mesh estimation methods on various benchmark datasets. The codes are
publicly available.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123520749.pdf

https://github.com/hongsukchoi/Pose2Mesh_RELEASE

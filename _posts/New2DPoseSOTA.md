#### Differentiable Hierarchical Graph Grouping for Multi-Person Pose Estimation

Multi-person pose estimation is challenging because it localizes body keypoints for multiple persons simultaneously. Previous methods can be divided into two streams, i.e. top-down and bottom-up methods. The top-down methods localize keypoints after human detection,
while the bottom-up methods localize keypoints directly and then cluster/group them for different persons, which are generally more efficient
than top-down methods. However, in existing bottom-up methods, the
keypoint grouping is usually solved independently from keypoint detection, making them not end-to-end trainable and have sub-optimal performance. In this paper, we investigate a new perspective of human part
grouping and reformulate it as a graph clustering task. Especially, we propose a novel differentiable Hierarchical Graph Grouping (HGG) method
to learn the graph grouping in bottom-up multi-person pose estimation
task. Moreover, HGG is easily embedded into main-stream bottom-up
methods. It takes human keypoint candidates as graph nodes and clusters keypoints in a multi-layer graph neural network model. The modules
of HGG can be trained end-to-end with the keypoint detection network
and is able to supervise the grouping process in a hierarchical manner. To
improve the discrimination of the clustering, we add a set of edge discriminators and macro-node discriminators. Extensive experiments on both
COCO and OCHuman datasets demonstrate that the proposed method
improves the performance of bottom-up pose estimation methods.

http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123520698.pdf

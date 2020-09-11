#### A Comprehensive Study of Weight Sharing in Graph Networks for 3D Human Pose Estimation

Graph convolutional networks (GCNs) have been applied to
3D human pose estimation (HPE) from 2D body joint detections and
have shown encouraging performance. One limitation of the vanilla graph
convolution is that it models the relationships between neighboring nodes
via a shared weight matrix. This is suboptimal for articulated body modeling as the relations between different body joints are different. 
The objective of this paper is to have a comprehensive and systematic study of
weight sharing in GCNs for 3D HPE. We first show there are two different ways to interpret a GCN depending on whether feature transformation 
occurs before or after feature aggregation. These two interpretations
lead to five different weight sharing methods, and three more variants
can be derived by decoupling the self-connections with other edges. We
conduct extensive ablation study on these weight sharing methods under controlled settings and obtain new conclusions that will benefit the
community.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123550324.pdf

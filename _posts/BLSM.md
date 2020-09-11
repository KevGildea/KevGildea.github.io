#### BLSM: A Bone-Level Skinned Model of the Human Mesh

We introduce BLSM, a bone-level skinned model of the human body mesh where bone scales are set prior to template synthesis,
rather than the common, inverse practice. BLSM first sets bone lengths
and joint angles to specify the skeleton, then specifies identity-specific
surface variation, and finally bundles them together through linear blend
skinning. We design these steps by constraining the joint angles to respect
the kinematic constraints of the human body and by using accurate mesh
convolution-based networks to capture identity-specific surface variation.
We provide quantitative results on the problem of reconstructing a collection of 3D human scans, and show that we obtain improvements in
reconstruction accuracy when comparing to a SMPL-type baseline. Our
decoupled bone and shape representation also allows for out-of-box integration with standard graphics packages like Unity, facilitating full-body
AR effects and image-driven character animation. Additional results and
demos are available from the project webpage: http://arielai.com/blsm

http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123500001.pdf

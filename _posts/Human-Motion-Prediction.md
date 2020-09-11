#### Learning Progressive Joint Propagation for Human Motion Prediction

Despite the great progress in human motion prediction, it
remains a challenging task due to the complicated structural dynamics of human behaviors. In this paper, we address this problem in three
aspects. First, to capture the long-range spatial correlations and temporal dependencies, we apply a transformer-based architecture with the
global attention mechanism. Specifically, we feed the network with the
sequential joints encoded with the temporal information for spatial and
temporal explorations. Second, to further exploit the inherent kinematic
chains for better 3D structures, we apply a progressive-decoding strategy, which performs in a central-to-peripheral extension according to the
structural connectivity. Last, in order to incorporate a general motion
space for high-quality prediction, we build a memory-based dictionary,
which aims to preserve the global motion patterns in training data to
guide the predictions. We evaluate the proposed method on two challenging benchmark datasets (Human3.6M and CMU-Mocap). Experimental
results show our superior performance compared with the state-of-the-art
approaches.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123520222.pdf

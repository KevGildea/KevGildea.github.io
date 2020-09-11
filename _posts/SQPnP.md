#### A Consistently Fast and Globally Optimal Solution to the Perspective-n-Point Problem

An approach for estimating the pose of a camera given a set
of 3D points and their corresponding 2D image projections is presented.
It formulates the problem as a non-linear quadratic program and identifies regions in the parameter space that contain unique minima with
guarantees that at least one of them will be the global minimum. Each
regional minimum is computed with a sequential quadratic programming
scheme. These premises result in an algorithm that always determines
the global minima of the perspective-n-point problem for any number
of input correspondences, regardless of possible coplanar arrangements
of the imaged 3D points. For its implementation, the algorithm merely
requires ordinary operations available in any standard off-the-shelf linear
algebra library. Comparative evaluation demonstrates that the algorithm
achieves state-of-the-art results at a consistently low computational cost.

http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123460460.pdf

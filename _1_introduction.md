# 1 Introduction

Digital image correlation (DIC) technique is a powerful experimental tool for measuring full-field
displacements and strains. Most current DIC algorithms can be categorized into either local or
finite-element-based global methods, see Fig. 1. As with most experimental approaches, there
are drawbacks with each of these methods. In the local method the subset deformations are estimated independently and the computed displacement field may not necessarily be kinematically
compatible. Thus, the deformation gradients can be noisy, especially when using small subsets.
Although the global method often enforces kinematic compatibility, it generally incurs substantially
greater computational costs than its local counterpart, which is especially significant for large data
sets. Recently, we have presented a new hybrid DIC algorithm, called augmented Lagrangian
digital image correlation (ALDIC) [1, 2], which combines the advantages of both the local (fast
computation times) and global (compatible displacement field) methods.
ALDIC code is freely available at Github and MATLAB File Exchange (link: [3]). We demonstrated
that our ALDIC algorithm has high accuracy and precision while maintaining low computational
cost, and is a significant improvement compared to current local and global DIC methods. For a
review of both local and global DIC methods, and details of this new proposed ALDIC method,
please see our paper [1] (full text can also be requested at [4]).
In addition, we also provide the finite-element-based global DIC (FE-Global-DIC) MATLAB code as
an open source to the community. This manual is to guide users/readers to run the finite-elementbased global DIC method.

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_main_gbdic.png">
</p>

Figure 1: (a) Schematic showing a DIC reference image f(X), with a general speckle pattern,
deforming into the deformed image g(y(X)) under some mapping y. X and y coordinates are in
the reference and deformed images, respectively. (b) A schematic comparison between the local
DIC method (left), where all the subsets are analyzed independently, and the finite-element-based
global DIC method (right), where a global basis set is used to represent the full-field deformation.

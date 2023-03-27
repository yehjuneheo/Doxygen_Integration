# 6 Code Section 4: Finite-element-based Global DIC iterations

## 6.1 Finite element DIC method math formulation
In the finite element based global DIC method, we represent the global deformation using a global
basis set, often based on a finite element formulation [13], i.e.,

eq3

where ψp
(X) are chosen global 4-node quadrilateral (Q4) finite element basis functions and up are
the unknown degrees of freedom. To minimize the DIC correlation function, for example,

eq4

we can solve this problem iteratively by setting uk+1 = uk + δu using the first order approximation

eq5

such that

eq6

This leads to a linear equation in δu

eq7

where

eq8
eq9

Different from conventional finite element analysis where numerical integrals can computed using
several Gauss points, here, we use pixel-wise summation to approximate numerical integrals in
equations (8-9).


## 6.2 Regularization technique
To speed up the convergence and reduce the noise, we could add regularization penalties onto
the DIC correlation function (4).

eq10

where α is the coefficient of the added gradient regularizer term 3
. For example, user can set α as
a fixed value. In the heterogeneous fracture demo case, if we set α = 10, set the iteration stopping
tolerance as 1e-4, and execute this section, then we will have the following lines displayed on the
MATLAB command screen where FE-Global-DIC iterates 11 steps and gets converged.

1 %% Section 4
2 fprintf (’ ------------ Section 4 Start ------------ \n’)
3 % %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
4 % Finite element based global DIC iterations
5 % %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
6 DICpara . tol = 1e -4; % iteration stopping threshold
7 alphaList = 10; % Set regularization coefficient , alpha , as 10

1 ------------ Section 4 Start ------------
2 --- Global IC - GN iterations ---
3 normW = 0.41832 at iter 1; time cost = 47.4258 s
4 normW = 0.040996 at iter 2; time cost = 38.4114 s
5 normW = 0.014932 at iter 3; time cost = 39.9557 s
6 normW = 0.0067409 at iter 4; time cost = 39.4569 s
7 normW = 0.0032884 at iter 5; time cost = 38.5084 s
8 normW = 0.0016662 at iter 6; time cost = 39.3641 s
9 normW = 0.00086242 at iter 7; time cost = 38.8785 s
10 normW = 0.0004522 at iter 8; time cost = 40.3063 s
11 normW = 0.00023907 at iter 9; time cost = 38.8822 s
12 normW = 0.00012706 at iter 10; time cost = 38.8817 s
13 normW = 6.777 e -05 at iter 11; time cost = 39.1988 s
14 Elapsed time is 439.2666 seconds .
15 ------------ Section 4 Done ------------

## 6.3 Find the best coefficient of the regularizer
Theoretically, with a smaller value of α, the solved displacements and strains are noisier and
there are less effects of the added regularization terms (see Fig. 12(a)). A large value of α may
oversmooth the deformation fields, which are preferred by the added regularization penalties (see
Fig. 12(c)). In practice, finding the best coefficient of the added regularizer term, α, needs user’s
experience or other optimization process 4
. Here, we also provide the code to estimate the best
value of α from the modified L-curve method [15]. User needs to uncomment the following line,
then the code will tune the best value of α automatically, see Fig. 13.

<p align="center" margin-bottom="20px">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\graph_1.png">
</p>
Figure 11: FE-Global-DIC converges after 11 iterations when α = 10.

1 % ====== Tune regularization coefficient ======
2 % If you don ’t know the best alpha ( coefficient ), please run the following
3 % codes to tune the best value of the coefficient of the regularizer | grad
u |^2) :
4 % %%%%% Uncomment the following line to tune the best value of alpha %%%%%%
5 alphaList = [1 e -3 ,1 e -2 ,1 e -1 ,1 e0 ,1 e1 ,1 e2 ,1 e3 ]* mean ( DICpara . winstepsize ) ;
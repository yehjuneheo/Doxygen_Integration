# 8 Code Section 6: Compute stress

If the material constitutive relation of the specimen is known, the relevant stress field in DIC experiment can be obtained from the calculated strain field.
For example, the constitutive equation in plane stress case reads as (Voigt’s notation):

eq11

where E is Young’s modulus, ν is Poisson’s ratio, γxy is the engineering shear strain equals two
times of infinitesimal shear strain εxy.
Similarly, the constitutive equation in plane strain case reads as (Voigt’s notation):

eq12

1 ------------ Section 6 Start ------------
2 Material model to compute Cauchy stress fields :
3 1: Linear elasticity -- Plane stress
4 2: Linear elasticity -- Plane strain
5 3: Others : User needs to edit codes in ./ plotFiles / Plotstress . m
6 Input here : 1
7 -------------------------------------
8 Define Linear elasticity parameters
9 Young ’ s modulus ( unit : Pa ) :
10 Input here ( e . g . , 69 e9 ) : 69 e9
11 Poisson ’ s ratio :
12 Input here ( e . g . , 0.3) : 0.3
13 -------------------------------------
14 Current image frame #: 2/2
15 ------------ Section 6 Done ------------

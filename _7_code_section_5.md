# 7 Code Section 5: Compute strains

## 7.1 Smooth displacement field if needed
Before computing strains, solved displacement fields can be further denoised if necessary. In
most cases, FE-Global-DIC with regularization solved displacement fields are already denoised,
so usually there is no need to further smooth solved displacement fields anymore.

1 ------------ Section 5 Start ------------
2 Do you want to smooth displacement ? (0 - yes ; 1 - no ) 1

If you put in “ 0 ”, a Gaussian smooth filter with standard deviation 0.5 will be applied. If a stronger
smoothing filter is needed, please edit the Gaussian filter parameters “ DispFilterSize ”, and “
DispFilterStd ”.

## 7.2 Compute strain fields
In FE-Global-DIC algorithm, strain fields can be further computed at finite element Gauss points.
Strain values at nodal points are extrapolated and averaged from the inside Gauss points. In

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_diff_alpha_backup.png">
</p>
Figure 12: FE-Global-DIC method solved displacement and strain fields with different regularization coefficients, α. With a smaller value of α, the solved displacements and strains are noisier,
while a large value of α may oversmooth the deformation fields.

addition, strain fields can also be computed from numerically differentiating solved displacement
field. In summary, we implement three methods to compute strain fields.
(0) Strain field can be computed from finite element Gauss points;
(1) Central finite difference of solved displacement field;
(2) Plane fitting method to differentiate solved displacement field. In this method, you will be
asked to input half plane width to define the size of the fitted plane;

1 What method to use to compute strain ?
2 0: Finite element ( Recommended ) ;
3 1: Finite difference ;
4 2: Plane fitting ;

<p align="center">
  <img src="C:\Users\yehju\Documents\Research_Doxygen\images\tables_1.png">
</p>
Figure 13: Finding the best coefficient of the regularization by the L-curve method. (a-b) Plots of
terms |u − u0| and |∇u|. Red dashed line in (b) points out the best α in the L-curve method, which
is equivalent to the plot in (c) for the “|u−u0|+β|∇u|”, where the minimizer corresponds to the best
α. Here, β is an empirical number here I set as the finite element size (β = 10 in the heterogeneous
fracture example, which is also the chosen finite element size). To further improve the accuracy of
α, I apply a quadratic polynomial to interpolate the data points near the best triangle point in (c),
and to further update α with the minimizer of the local quadratic polynomial function.

5 Input here : 0

If user inputs “ 2 ”, MATLAB command window will display following lines for continuing to define
the plane size:
1 What is your half window size : % Input half window size for plane fitting
Three popular types of strains are implemented: infinitesimal strain, Eulerian strain based on
deformed configuration, and finite Green-Lagrangian strain.

1 Infinitesimal stran or finite strain ?
2 0: Infinitesimal stran ;
3 1: Eulerian strain ;
4 2: Green - Lagrangian strain ;
5 3: Others : code by yourself ;
6 Input here : 0

## 7.3  Plot and save results
Users can visualize solved displacement and strain field and plot them overlaid with original DIC
images, see Fig. 14. Finally, don’t forget to save results for future use.

1 Save figures into different format :
2 1: jpg ( Choose transparency 0~1)
3 2: pdf ( Choose transparency = 0)
4 3: Others : Edit codes in ./ plotFiles / SaveFigFiles . m
5 Input here :

Current version code, overlaying original DIC image can only be saved in the “jpg” format.

1 Define transparency for overlaying original images :
2 Input a real number between 0( Only original images )
3 and 1( Only deformation results ) .
4 Input here ( e . g . 0.5) : 0.5

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_gb_frac_final_plots.png">
</p>
Figure 14: Final 2D FE-Global-DIC code tracked deformation fields with original DIC images overlaid as the background. (a) x-displacement; (b) y-displacement; (c) equivalent von Mises strain;
(d-f) infinitesimal strains exx, exy, and eyy; (g-h) maximum and minimum principal strains; (i) max
shear strain.

Finally, all the results will be saved in a Matlab matfile, see Table 3.

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\table_3.png">
</p>

1 %% Save data again including strain solve method
2 results_name = [’ results_FE_globalDIC_ ’, imgname ,’_st ’,num2str ( DICpara .
winstepsize ) ,’_alpha ’,num2str ( DICpara . alpha ) ,’. mat ’];
3 save ( results_name , ’file_name ’,’DICpara ’,’DICmesh ’,’ResultDisp ’,’
ResultDefGrad ’,’ ResultStrain ’,’ResultFEMesh ’ ,...
4 ’normOfW ’,’timeICGN ’) ;

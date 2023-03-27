# 5  Code Section 3: Computing an initial guess of unknown deformation from FFT-based cross correlation

## 5.1 FFT-based methods to compute initial guess
In this section, the initial estimate of the unknown displacement is calculated by maximizing the
(zero-normalized) cross correlation function CZNCC, see Fig. 8(a-b).

eq1

where µf
, µg are average grayscale values of DIC images, f and g; σf
, σg are the standard deviation
of image grayscale values. Above cross correlation can be computed fast using Fourier transform
convolution theorem and fast Fourier transform (FFT). For example:

eq2

where F[·] denotes the Fourier transform, (·) denotes the complex conjugate, and “◦” denotes the
Hadamard product (entry-wise product) and the absolute values are taken entry-wise as well.
The ALDIC code provides three ways to compute the initial guess for an unknown displacement
field, as shown in Fig. 8(c-e), and following lines will appear on the screen:

1 --- Method to compute an initial guess of displacements ---
2 0: Multigrid search based on an image pyramid
3 1: Whole field search for all the subsets
4 2: Search near manually clicked seeds and then interpolate for the
full - field
5 Input here :

Method 1 (whole field search, Fig. 8(c)) executes FFT-based cross correlation for all local subsets
(subsets can overlap), while Method 2 (Several seeds search, Fig. 8(d)) is to compute near several
manually clicked local seeds. Both Methods 1 & 2 will ask the user to enter the size of the search
area. The user should try to search for a small value of the search area size and incrementally
increase that value until it exceeds the maximum x- and y-displacements. For example, in the
heterogeneous fracture example as shown in Fig. 10, the max magnitude of the displacements are
around 60 px, thus the search area size can be chosen as an integer larger than 60 . If the chosen
FFT search area size is too small, for example, 30 or 50 , the computed initial displacements
will be noisy (see Fig. 9(a-b)). If this happens, the user needs to continually increase the size of
the search area until a good initial guess is found. For example, search area size equals 60 in
Fig. 9(c).

1 --- What is your initial guess search zone size ( pixels ) ? ---
2 User should start to try a small integer value , and gradually increase the
3 value of the search zone size until it is larger than the magnitudes of
4 | disp u | and | disp v |.
5 Input here : 60
6 Finish initial guess search !

To further speed up the above FFT-based optimization process, we also provide a multigrid Method
0 based on the constructed image pyramids (see Fig. 8(e)). There is no need to provide the search
area size in this Method. For example, an initial guess of the above heterogeneous fracture deformation is solved and shown in Fig. 10.

<p align="center">
  <img src="C:\Users\yehju\Documents\Research_Doxygen\images\2d_init.png">
</p>
Figure 8: (a-b) The initial estimate of the unknown displacement of a local subset is calculated
by maximizing the (zero-normalized) cross correlation function. (c-d) All local subsets or a few
manually clicked seeds are analyzed using FFT-based cross correlation to compute the initial
guesses of their deformations. (e) A multigrid method based on the constructed image pyramids
is proposed to compute the initial estimate of full-field deformation.

<p align="center">
  <img src="C:\Users\yehju\Documents\Research_Doxygen\images\2d_init_fft_size.png">
</p>
Figure 9: Method 1 solved displacement fields by the FFT-based cross correlation method with
different search area sizes. (a-b) If the chosen size of the search area is too small, computed initial
displacements will be super noisy. (c) A good “search area size” should not be smaller than the
magnitudes of displacement components (|dispu|, |dispv|).

<p align="center">
  <img src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_fft_init_guess.png">
</p>
Figure 10: Method 0 – Multigrid FFT-based cross correlation solver – computed initial estimate of
the unknown deformation field.


## 5.2 Remove noise in computed initial gues
In practice, FFT-based cross correlation method solved initial guess 2 may have large noise, the
user can further remove these bad points by applying a median filter, setting a q-factor threshold,
and setting upper and lower limits of displacements. Users can also continue to delete the bad
points directly by clicking them in each image and then press the ” Enter ” key. However, this step
requires some manual work. If noise elimination is necessary, the user can follow the following
steps:

1 Do you clear bad points by setting upper / lower bounds once more ?
2 (0 - yes ; 1 - no )

If the user inputs ” 0 ”, then he/she will be asked to enter the upper and lower limits of the x- and
y-displacements. If the user inputs ” 1 ”, this process will be skipped.

1 % ======= Find bad initial guess points manually by setting bounds =======
2 What is your upper bound for x - displacement ?
3 What is your lower bound for x - displacement ?
4 What is your upper bound for y - displacement ?
5 What is your lower bound for y - displacement ?
6 Do you clear bad points by setting upper / lower bounds ? (0 - yes ; 1 - no )

Besides setting upper and lower bounds to remove local bad points, we can continue removing
bad points directly by clicking them in the image.

1 % ======= Find bad initial guess points manually =======
2 ’Do you clear bad points by directly pointing x- disp bad points ?
3 (0 - yes; 1 -no)’;
4 ’Do you clear bad points by directly pointing y- disp bad points ?
5 (0 - yes; 1 -no)’;

Click all the bad points directly, and then press the ” Enter ” key.
At the end of this section, a finite element mesh is also automatically generated.

1 --- Finish setting up mesh and assigning initial value ! ---

The image pixel grayscale gradient can also be calculated fast by using a finite difference operator
and convolution operation.

1 --- Start to compute image gradients ---
2 --- Computing image gradients done ---


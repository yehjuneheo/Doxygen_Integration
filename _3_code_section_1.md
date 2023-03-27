# 3 Code Section 1. MATLAB mex setup

Execute this section and we will try to build “mex” functions from C/C++ source codes for image
grayscale value interpolation, where linear, bi-cubic (by default) and bi-cubic splines interpolations

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_mexCheck.png">
</p>
Figure 3: Message display on the command window when a mex C/C++ compiler is stalled successfully.

are implemented in this code. For example, by default we use bi-cubic interpolations where the
associated mex set up file is called “ba interp2.cpp” [6].


## 3.1 Test MATLAB mex setup
First, we test whether there is already a C/C++ compiler installed on your computer by inputting
mex -setup and press Enter key on the MATLAB command window. If an available C/C++ compiler is already installed, please skip Section 3.2 and jump to Section 3.3.

## 3.2 Test MATLAB mex setup
The step of installing mex C/C++ compilers is a common step for users to run C/C++ codes with
MATLAB. Mac users usually don’t come across the error message from mex C/C++ compilers.
For Windows users, you can follow these steps to install mex C/C++ compiler. More details can
be found in [7, 8].
• Download: TDM-gcc compiler from: http://tdm-gcc.tdragon.net/
• Install TDM-gcc compiler on your computer. For example, I install it at ’C:\TDM-GCC-64’ 1
.
• Restart MATLAB and input these codes on the command window:
setenv(’MW_MINGW64_LOC’,’YourTDMGCCPath’); mex -setup;
to check whether ”mex” is set up successfully or not. Don’t forget to replace the above
’YourTDMGCCPath’ using your own installation location of TDM-gcc package in the last step.
For example, if it’s installed at ’C:\TDM-GCC-64’, please replace previous ’YourTDMGCCPath’
with ’C:\TDM-GCC-64’. If a mex C/C++ compiler is installed successfully, a message similar
to (Fig. 3) will display on the MATLAB command window.

(a)
<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_ex_sec1_1.png">
</p>
(b)
<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_ex_sec1_2.png">
</p>

Figure 4: FE-Global-DIC code Section 1 is executed successfully and a message similar to (a) or
(b) will display on the command window.


## 3.3 Execute code section 1
Once a mex C/C++ compiler is installed, we can execute main FE GlobalDIC.m code Section 1
and a successful message will display on the MATLAB command window, see Fig. 4.


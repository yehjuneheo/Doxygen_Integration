# 4 Code Section 2. Load images and set up DIC parameters & mesh

This section is to load DIC reference and deformed images and set up DIC parameters. First,
please put your images on the MATLAB working path. After executing this section, all the FEGlobal-DIC associated parameters will be stored in the workspace in “DICpara”. All the mesh
properties will be stored in “DICmesh” after executing code Section 3. Here we make a brief
summary of both these two data structures in Table 1 and Table 2.

<p align="center" margin-bottom="20px">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\table_1.png">
</p>

<p align="center" margin-bottom="20px">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\table_2.png">
</p>

## 4.1  Load DIC images
MATLAB command screen displays these lines to allow user to select their choice to load DIC
images, which will be explained in Section 4.1.1-4.1.3.

1 ------------ Section 2 Start ------------
2 Choose method to load images :
3 0: Select images folder ;
4 1: Use prefix of image names ;
5 2: Manually select images .
6 Input here :

One comment for the FE-Global-DIC code is that it always manipulate the deformed images and
tries to transform them back to the reference image to compute their deformation fields which is
based on the Lagrangian description. If user wants to track the deformation field in the Eulerian
description, user can select the reference image as the second image, and select the deformed
image as the first image and manipulate the reference image to transform to the current deformed
image.


### 4.1.1 Load DIC images from certain folder
If we select method 0: Select images folder to load DIC images, you will be asked to select
the folder path, and all the images within this folder will be loaded automatically. In the cumulative
DIC mode, the first frame is set to be the fixed reference image by default, while all the subsequent
frames in the image sequence are set to be deformed images whose deformations will be tracked
in the Lagrangian description. In the incremental DIC mode, the reference image can be updated
after every certain number (”DICpara.ImgSeqIncUnit”) of frames. After loading DIC images, please
jump to Section 4.2.


### 4.1.2 Load DIC images with prefix of image name
If we select method 1: Use prefix of image names to load DIC images, user also needs to
provide prefix text words of their DIC image frames (and all these images need to be added
to the MATLAB path as well). For example, if all the DIC images are named in the format as:
”img 0001.tif”, ”img 0002.tif”, · · · , use should input ” img_0*.tif ” on the MATLAB command
screen to load all the DIC images started with prefix ”img 0” and in the ”tif” format. After loading
DIC images, please jump to Section 4.2.

1 What is prefix of DIC images ? E . g . img_0 *. tif .
2 Input here :


### 4.1.3 Load DIC images manually
If we select method 2: Manually select images , user needs to load DIC images frame by frame
manually, see Fig. 6. FE-Global-DIC code sets the first loaded image as reference image and
other images as deformed images by default.
1 --- Please load first image ---
2 --- Please load next image ---
3 Do you want to load more deformed images ? (0 - yes ; 1 - no )
Input ” 0 ” if you want to continue uploading images and input ” 1 ” if you want to stop uploading
images. For example, we can select first reference image as ”img 0000.tif”, and select second
image as ”img 0570.tif”.

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_load_img_folder.png">
</p>
Figure 5: Load DIC iamges by selecting the folder including all DIC images. For example, after
clicking chosen folder ”Images frac heter”, all the images in this folder will be loaded automatically.

## 4.2 Define region of interest (ROI)
Execute code Section 2, user can click both the top-left and bottom-right corner points on a
popped-out image to define DIC region of interest (ROI). On the command window, it displays:
1 --- Define ROI corner points at the top - left and the bottom - right ---
Then user first click a left-top point and then click a right-bottom point to define ROI directly on the
DIC image, see Fig. 7.

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_load_img_manual.png">
</p>
Figure 6: Manually load DIC images by clicking both reference and deformed images

After clicking both the top-left and bottom-right corner points, the command window screen will
display their coordinates in the unit of pixels. E.g., in the image shown in Fig. 7, I define a ROI with
top-left and bottom-right corner points are:
1 Coordinates of top - left corner point are (322.786 ,74.730)
2 Coordinates of bottom - right corner point are (750.063 ,1128.439)
Comment 1: If the top-left or bottom-right corner point is clicked out of the image, it will be adjusted
to the nearest point on the original DIC image borders automatically.
Comment 2: If user prefers to putting in ROI coordinates instead of directly clicking corner points
on the DIC image. Please uncomment line % gridxROIRange = [gridxROIRange1, gridxROIRange2];
% gridyROIRange = [gridyROIRange1, gridyROIRange2]; and modify values of ”gridxROIRange”
and ”gridyROIRange” there.

<p align="center">
  <img width="538" src="C:\Users\yehju\Documents\Research_Doxygen\images\fig_def_ROI_click_corner_pts.png">
</p>
Figure 7: Manually click top-left and bottom-right corner points to define DIC region of interest
(ROI).

## 4.3 Set up DIC parameters
Then user will be asked to decide the finite element size. Current version of this code uses uniform
square Q4 FE-meshes.

1 --- What is the finite element size ? ( unit : px ) ---
2 Input here : 10

## 4.4 Additional parameters setup when dealing with image sequence
If we upload an image sequence with more than two frames, as for each new frame, we can
choose to use the displacement results in last frame as the initial guess for the new image frame,
or we can just redo FFT initial guess for every new frame. This choice depends on how big relative
displacements can be between two consecutive frames. Generally, if the relative displacement
field between two consecutive frames is smaller than 5-7 voxels, we can use the deformation result
of last frame as the initial guess displacement field for the new frame; otherwise it is suggested
that we still need to redo the FFT initial guess process.

1 Since we are dealing with an image sequence with multiple frames , for each
new frame , do we use the result of last frame as an initial guess or
redo FFT initial guess for every new frame ?
2 0: Use last frame ;
3 1: Redo initial guess .
4 Input here :

When post-process image sequence with more than two frames, user could decide to perform
either cumulative mode DIC or incremental mode DIC. The cumulative mode is the default setup
and all the following frames will be compared with the first frame. However, incremental mode is
preferred when dealing with extremely large deformations but may lose some accuracy because
of the reference image has been updated. We recommend the user to try cumulative mode first,
and if cumulative mode doesn’t work very well, then try incremental mode. If you choose to use
incremental mode, you will further be inquired to input how often you would like to update the
reference image:

1 --- Choose cumulative or incremental mode ---
2 0: Cumulative ( By default ) ;
3 1: Incremental ;
4 Input here : 1

If you choose to use incremental mode, you will further be inquired to input how often you would
like to update the reference image:

1 Incremental mode : How many frames to update reference image once ?
2 Input here : 10

E.g., I want to update my reference image once every ten frames, so I input: 10 . The minimum
number you can input is 1 , which means to update reference image every frame.
Every time the reference image is updated, you can choose to update the region of interest (ROI)
at the same time or not. To achieve this, user will be asked as follows:

1 Update ROI at the same time of updating reference image ?
2 0: Do not update ROI ;
3 1: Manually ( Recommended ) ;
4 2: Automatically ;
5 Input here : 1

E.g., Input 1 or 2 if you want to update ROI at the same time of updating reference image.
Theoretically, this ROI update can be done automatically using the solved deformation of the last
frame. However, we find it is most robust to update this ROI manually.

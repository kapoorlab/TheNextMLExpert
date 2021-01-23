# TheNextMLExpert
Solving the Next ML expert challenge

Task 1) Segmentation of Nuclei
1) Perform sum projection of the nuclei images and store them in a directory with same name as the unprojected images.

2) Use the Jython code to convert Rois to binary mask, then manually make cuts to seperate the overlapping nuclei.

3) Denoise the Raw images using CARE model and train UNET model for Denoised Raw to Binary Mask and Stardist model for Denoised Raw to label(Binary Mask) using this notebook:

4) Apply the segmented model slice by slice stitching the slices using RelabelZ function written by me and Volker H.



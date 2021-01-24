# TheNextMLExpert
Solving the Next ML expert challenge

Task 1) Segmentation of Nuclei
1) Perform sum projection of the nuclei images and store them in a directory with same name as the unprojected images.

2) Use the [Jython code](https://github.com/kapoorlab/TheNextMLExpert/blob/main/CreateTrainingData/FMIChallengeRoitoMask.py) to convert Rois to binary mask, then manually make cuts to seperate the overlapping nuclei.

3) Denoise the Raw images using [CARE model](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/ZYXDenoising.ipynb) 
use the denoised and raw images to train UNET and Stardist model, [training notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/TrainModel.ipynb)

4) Using seeds from stardist perfrom a marker controlled watershed using UNET mask, [prediction notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/SmartSeedsPrediction.ipynb)

5) Stitch the nearby cells to create a 3D object in the same notebook.

 Tif file of Segmentation Results: [UNET, StarDist and SmartSeeds](https://drive.google.com/drive/folders/1I4osUmRQqqEUjJYRsA4ujwVrBGxWmKEz?usp=sharing)

6) [Notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/NapariCorrectionTool.ipynb) for comparing nuclei segmentation between StarDist and SmartSeeds along with Spot Segmentation result. The idea is to correct the mistakes in smartseeds segmentation to train a real 3D UNET and Stardist 3D model.


7) The h5 files of [Trained Models](https://drive.google.com/drive/folders/1G9oAPFxHTGedwWSoXgzAX3fd6WzXIspA?usp=sharing), the training parameters are specified in
the [training notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/TrainModel.ipynb).

Task 2) Spot Segmentation
Method A:
1) I made an MSER based interactive Fiji plugin to segment spots in 3D. It requires installation of two jars [MSERPlugin](https://github.com/kapoorlab/TheNextMLExpert/blob/main/SpotSegmentationMSER/MSER_-1.0.0.jar) and [MasterPanels](https://github.com/kapoorlab/TheNextMLExpert/blob/main/SpotSegmentationMSER/MasterPanels-1.0.0.jar)
If this installation does not work try downloading the jars from here: [Alternate jars](https://drive.google.com/drive/folders/1Ge1p8x2ZNRy3GxS0QlrYis9i7u7suZOV?usp=sharing)
2) After installing these two jars in Fiji, I used these [parameters](https://github.com/kapoorlab/TheNextMLExpert/blob/main/Screenshots/MSERPanel.png) to make the component tree.

Method B:
1) I trained a pixel classifier using Ilastik to obtain 3D labelled segmentation image of the spots.


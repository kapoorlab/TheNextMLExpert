# TheNextMLExpert
Solving the Next ML expert challenge

Task 1) Segmentation of Nuclei
1) Perform sum projection of the nuclei images and store them in a directory with same name as the unprojected images.

2) Use the [Jython code](https://github.com/kapoorlab/TheNextMLExpert/blob/main/CreateTrainingData/FMIChallengeRoitoMask.py) to convert Rois to binary mask, then manually make cuts to seperate the overlapping nuclei.

3) Denoise the Raw images using [CARE model](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/ZYXDenoising.ipynb) 
use the denoised and raw images to train UNET and Stardist model, [training notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/TrainModel.ipynb)

4) Using seeds from stardist perform a marker controlled watershed using UNET mask, slice by slice 2D result [prediction notebook](https://nbviewer.jupyter.org/github/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/SmartSeedsPrediction.ipynb)

5) Stitch the nearby cells to create a 3D object in the same notebook, using a pre set distance threshold.

 Tif file of Segmentation Results: [UNET, StarDist and SmartSeeds](https://drive.google.com/drive/folders/1I4osUmRQqqEUjJYRsA4ujwVrBGxWmKEz?usp=sharing)

6) [Notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/NucleiSegmentations.ipynb) for comparing nuclei segmentation between StarDist and SmartSeeds. The idea is to correct the mistakes in smartseeds segmentation using the Napari correction tool I provide here to train a real 3D UNET and Stardist 3D model.


7) The h5 files of [Trained Models](https://drive.google.com/drive/folders/1G9oAPFxHTGedwWSoXgzAX3fd6WzXIspA?usp=sharing), the training parameters are specified in
the [training notebook](https://github.com/kapoorlab/TheNextMLExpert/blob/main/NucleiSegmentation/TrainModel.ipynb).

Task 2) Spot Segmentation
Method A:
1) I made an MSER based interactive Fiji plugin to segment spots in 3D. It requires installation of two jars [MSERPlugin and MasterPanels](https://github.com/kapoorlab/TheNextMLExpert/tree/main/MSER-FijiJars) 
If this installation does not work try downloading the jars from here: [Alternate jars](https://drive.google.com/drive/folders/1Ge1p8x2ZNRy3GxS0QlrYis9i7u7suZOV?usp=sharing)
2) After installing these two jars in Fiji, I used these [parameters](https://github.com/kapoorlab/TheNextMLExpert/blob/main/Screenshots/MSERPanel.png) to make the component tree.

Method B:
1) I trained a pixel classifier using Ilastik to obtain two channel image contaninng class probabilities for spots and background.
2) Using a probability and size thereshold I converted the first channel (spot probability) into binary image and then to label image.
3) Then using this [notebook](https://nbviewer.jupyter.org/github/kapoorlab/TheNextMLExpert/blob/main/SpotSegmentation/ILASTIK-MSERSegmentationSpots.ipynb) I compare the two segmentations and the results are comparable with Ilastik pixel classification producing slightly better results than MSER, with more annotations of the classes the pixel calssification workflow can be improved further to get even better spot probabilities.

Tracking: 

After obtaining the segmentation results for spots and the nuclei, the goal is to track the spots inside each nuclei. However since complete timelapse was not provided in the assingment, I create a fake time lapse of image name ending in t38, 101, 106 and 141 to illustrate a proof of concept of tracking.
1) Make the fake [time lapse images](https://drive.google.com/drive/folders/1lvlZsG415gw6URIQJoIXtPaI8kTADnHZ?usp=sharing) of Raw, Spot segmentation and nuclei segmentation (masks) and run this notebook to convert the image data into [csv](https://github.com/kapoorlab/TheNextMLExpert/blob/main/Tracking/PythonTools/BTrackMateLocalization.ipynb) This csv makes the attributes required by BTrackmate to track cells inside a region. This csv file it creates can also be found in the same link folder. 

Challenge Answeres:

## Specific tasks

Q) Create an automated cell segmentation given the provided data and ground truth annotations

Q) Suggest ways to generate more ground truth, possibly in a semi-automated way

Q) Analyze the quality of your segmentation method and discuss possibilities to improve the result

A) Using 2D annotations train smart seeds required models (depth = 5, start filter = 48), using the 
Stitched integer labels, do some manual correction using the provided Napari correction notebook
to generate more ground truth data .
Using the new data do augmentations, denoising to create mode data and train a real 3D model


Q) Given the overall goal of a per-cell motion correction, discuss alternative approaches

A) Tracking is done inside the integer mask (nuclei), using the tracks of the cell we could make a front end
Python based solution to do the per-cell motion correction using the nuclei mask information.

Q) Discuss strategies for spot detection

A) Using MSER interactive plugin to obtain integer labelled 3D spot segmentations or using Ilastik to generate probability maps
of the spot class, which can then be converted to labelled 3D spot segmentations using the provided [notebooks](https://nbviewer.jupyter.org/github/kapoorlab/TheNextMLExpert/blob/main/SpotSegmentation/ILASTIK-MSERSegmentationSpots.ipynb)

Q) Assume that your workflow has spiked a lot of interest across different users/labs. Discuss how you could
  scale-up serving the workflow and identify potential challenges

A) Make the [jars](http://biii.eu/simple-mser-based-segmentation-tool-spot-detection-234d) available on Fiji update site and release the python tools using pip. For different final specific lab related
questions, create customised front end Jupiter notebooks to extract the information of interest, which is the only degenerate 
Step in otherwise universal workflow 

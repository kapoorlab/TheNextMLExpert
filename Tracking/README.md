# DeepLearningTracking

Tools for doing tracking using instance segmentation image using Fiji and Jupyter notebooks.

This is a pre-release tool for trying out tracking using BTrackMate workflow. To use this install the jars in Fiji and create an anaconda enviornment for Napari based visualization.

For creating napari based visualization:

1) conda create -n testenv python==3.9.0

2) conda activate testenv

3) pip install scikit-image napari==0.4.3 pyqt5 btrack natsort scipy opencv-python-headless tifffile matplotlib ffmpeg-python imageio_ffmpeg

4) Now input your raw image, instance segmentation image in 2D + t or 3D + t and optionally mask image in this notebook:
https://github.com/kapoorlab/DeepLearningTracking/blob/main/PythonTools/BTrackMateLocalization.ipynb. This notebok creates a csv file of cell attributes required by the Fiji tracker.

5) After creating a csv file that starts with Fiji{filename}.csv start Fiji, load Raw image and select BTrack - > XYZT tracker plugin

6) Load the input Raw image (you can skip loading the segmentation and mask image if you did step 4)

7) Load the csv file and click start Tracker, after that you will be lead into the usual TrackMate interface for tracking.

8) After doing the tracking/ track editing in TM save the xml file for visualization in Napari.

9) Load the saved XML in this notebook: https://github.com/kapoorlab/DeepLearningTracking/blob/main/PythonTools/BTrackMateVisualization.ipynb

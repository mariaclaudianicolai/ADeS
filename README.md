# ADeS
Detect apoptosis with ADES

![alt text](https://github.com/mariaclaudianicolai/ADeS/blob/main/pipeline_for_apoptosis_detection.jpg?raw=true)

# **Usage**

We provide an example of ADES application to predict apoptotic events.

We will apply ADES on a video 24 hours, with 250 frames in  _.tiff_  format, 1024x1024 resolution. We will expect ADES to predict apoptotic coordinates.

**Connect colab notebook to your Google Drive**

The following code will load the video and import the ADES code for you.

To run this example we move the video and the code in a folder in your Google Drive.

> #Connect to drive and import project with testing video
from google.colab import drive
drive.mount('/content/drive')
!cp /content/drive/MyDrive/path_to_ades_project/your_file.tif /content
!cp /content/drive/MyDrive/path_to_ades_project/ADES.zip /content
!unzip '/content/ADES.zip'
import ADES.ades

**Prediction with ADES**

Then, we predict the coordinates of apoptosis.

Here, we provide the confidence level at which we wish to discover apoptotic events as well as the frames to analyze (f1 is the start frame and f2 is the last frame).

>#Process time lapses with ades.predict
path = '/content/11_ori.tif'  # path of video in tif format
f1 = 1
f2 = 100  #range of frames to process
threshold = 0.95
predictions, movie = ADES.ades.predict(path,threshold,f1,f2) #process movies and predict apoptotic coordinates

**Save output video**

Then we can save the video generated by ADES to visualize the detection.

> # Save movie in mp4 format
> !pip install scikit-video
import skvideo.io
nF = movie.shape[0]
writer = skvideo.io.FFmpegWriter("test.mp4",inputdict={'-r': '10'},outputdict={'-r': '8'})
for i in  range(0,nF):
writer.writeFrame((movie[i, :, :, :]))
writer.close()

**Visualizing spatial-temporal distribution of apototic events**
To do

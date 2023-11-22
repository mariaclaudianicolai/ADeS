# ADeS
Intravital microscopy has revolutionized live cell imaging by allowing the study of spatial-temporal cell dynamics in living animals. However, the complexity of the data generated by this technology has limited the development of effective computational tools to identify and quantify cell processes. Amongst them, apoptosis is a crucial form of regulated cell death involved in tissue homeostasis and host defense. Live-cell imaging enabled the study of apoptosis at the cellular level, enhancing our understanding of its spatial-temporal regulation. However, at present, no computational method can deliver label-free detection of apoptosis in microscopy time-lapses. To overcome this limitation, we developed ADeS, a deep learning-based apoptosis detection system that employs the principle of activity recognition. We trained ADeS on extensive datasets containing more than 10,000 apoptotic instances collected both in vitro and in vivo, achieving a classification accuracy above 98% and outperforming state-of-the-art solutions. ADeS is the first method capable of detecting the location and duration of multiple apoptotic events in full microscopy time-lapses, surpassing human performance in the same task. We demonstrated the effectiveness and robustness of ADeS across various imaging modalities, cell types, and staining techniques. Finally, we employed ADeS to quantify cell survival in vitro and tissue damage in vivo, demonstrating its potential application in toxicity assays, treatment evaluation, and inflammatory dynamics. Our findings suggest that ADeS is a valuable tool for the accurate detection and quantification of apoptosis in live-cell imaging and, in particular, intravital microscopy data, providing insights into the complex spatial-temporal regulation of this process.

![alt text](https://github.com/mariaclaudianicolai/ADeS/blob/main/pipeline_for_apoptosis_detection.jpg?raw=true)

# **Usage**

We provide an example of ADES application to predict apoptotic events.

We will apply ADES on a video 24 hours, with 250 frames in  _.tiff_  format, 1024x1024 resolution. We will expect ADES to predict apoptotic coordinates.

**Connect colab notebook to your Google Drive**

The following code will load the video and import the ADES code for you.

To run this example, we move the video and the code in a folder in your Google Drive.

```
#Connect to drive and import project with testing video
from google.colab import drive
drive.mount('/content/drive')
!cp /content/drive/MyDrive/path_to_video_file/your_file.tif /content
!cp /content/drive/MyDrive/path_to_ades_project/ADES.zip /content
!unzip '/content/ADES.zip'
 
import ADES.ades
```

**Prediction with ADES**

Then, we predict the coordinates of apoptosis.

Here, we provide the confidence level at which we wish to discover apoptotic events as well as the frames to analyze (f1 is the start frame and f2 is the last frame).

```
#Process time lapses with ades.predict
path = '/content/file.tif'  # path of video in tif format
f1 = 1
f2 = 100  #range of frames to process
threshold = 0.95
predictions, movie = ADES.ades.predict(path,threshold,f1,f2) #process movies and predict apoptotic coordinates
```

**Save output video**

Then, we can save the video generated by ADES to visualize the detection.

```
#Save movie in mp4 format
!pip install scikit-video
import skvideo.io
 
nF = movie.shape[0]
writer = skvideo.io.FFmpegWriter("test.mp4",inputdict={'-r': '10'},outputdict={'-r': '8'})
for i in  range(0,nF):
writer.writeFrame((movie[i, :, :, :]))
writer.close()
```
The results are as follows:
![alt text](https://github.com/mariaclaudianicolai/ADeS/blob/main/results_example.png?raw=true)

**Visualizing spatial-temporal distribution of apoptotic events**
To do

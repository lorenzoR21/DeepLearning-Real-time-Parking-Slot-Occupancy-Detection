# Real-time Parking Slot Occupancy Detection
## Introduction
The idea of the project concerns parking occupancy detection using Deep Learning. The central theme of this project is the creation of a model that is able to identify in real-time, using images/videos of a real car park, which spaces are free and which are occupied.
This repository contains two different parts:
* [notebook](notebook): this folder contains the [main notebook](notebook/parking_slot_classification.ipynb) which concerns the creation and training of the model to classify the occupancy of parking slots in real-time.
* [implementation](implementation): this folder contains the implementation of an Android mobile app for searching for available parking slots and a script that uses the previously trained model to communicate, in real-time, to all app users which slots are free and which are occupied using video coming from a real parking camera.
## Dataset
[CNRPark+EXT](http://cnrpark.it) is a dataset for visual occupancy detection of parking lots of roughly 150,000 labeled images (patches) of vacant and occupied parking spaces, built on a parking lot of 164 parking spaces. Is composed by images collected from November 2015 to February 2016 under various weather conditions by 9 cameras with different perspectives and angles of view. CNR-EXT captures different situations of light conditions, and it includes partial occlusion patterns due to obstacles (trees, street lamps, other cars) and partial or global shadowed cars.

Parking Slots:

|  |  |  |  |
|:----:|:----:|:----:|:----:|
| <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/11busy.jpg" width="150" height="150"> | <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/13busy.jpg" width="150" height="150"> | <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/34busy.jpg" width="150" height="150"> | <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/38busy.jpg" width="150" height="150"> |
| <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/11empty.jpg" width="150" height="150"> | <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/13empty.jpg" width="150" height="150"> | <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/34empty.jpg" width="150" height="150"> | <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/38empty.jpg" width="150" height="150"> |

Entire Parking Images from two different cameras (parking slots are manually segmented using squared masks):

<img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/cam_a.jpg" width="400" height="300">                  <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/cam_b.jpg" width="400" height="300"> 


## Model
The [main notebook](notebook/parking_slot_classification.ipynb) contains the development and training of the real-time parking slot classification model. The model used is an improved version of the MobileNetV3 model. The model takes as input the images of the individual parking slots. In particular, the images of individual parking slots are extracted from images of entire parking lots using the coordinates of the individual parking slots. The extraction of the coordinates of the individual parking slots is done before the classification, it is possible to extract the coordinates manually (as is done in the CNRPark dataset) or using a support model that uses the pre-trained model FasterRCNN-FPN of pythorch ([support notebook](notebook/parking_slot_detection.ipynb)).
## Integration of the classification model with the mobile app
The Android application is an app that allows users to search for available parking near them. This is possible thanks to the trained real-time classification model of parking slots, which takes video input from a camera of a real parking lot. Using the coordinates of each parking slot, the individual parking slots are extracted from the video frames and classified as available or occupied (all this in real-time). The classification result is sent to the application database, and this allows application users to view in real-time which parking slots are available and which are occupied. This is in [implementation](implementation) folder. Below is an example of a frame from the parking video:

<img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/app_parking.jpg" width="200" height="444">   <img src="https://github.com/lorenzoR21/Computer-Vision-Project/blob/main/readme_images/ann_image.png" width="590" height="444">

## References
* [Parking Lot Occupancy Detection with Improved MobileNetV3](https://doi.org/10.3390/s23177642)
## Author
[Lorenzo Russo](https://github.com/lorenzoR21)

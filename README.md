# FindingLanes

## **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images. 

### Inputs

- The input images to the program are in the test_images folder. There are 6 images of drive lanes
- The input videos are in the folder test_videos folder. The folder contains 3 videos. However the program currently works only on 2 videos (solidWhiteRight.mp4 & solidYellowLeft.mp4). We will have to modify the processing pipleline to make it run on the Challenge.mp4

### Outputs

- The image & video outputs are in the test_images_output & test_videos_output respectively

### Code

The processing logic is present in the jupyter notebook p1.ipynb. This was run inside a docker container that came with CarND-Term1-Starter-Kit (from Udacity Self-Driving Car Engineering NanoDegree). The key portions of the code are:
- Lane Finding Pipeline
- process_image function
- draw_lines function (within the Helper Functions section)

### Documentation

The writeup_template gives you an overview of the pipeline and approach adopted

# **Finding Lane Lines on the Road** 


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/image1.jpg "Grayscale"
[image2]: ./examples/image2.jpg "Gaussian Blur"
[image3]: ./examples/image3.jpg "Canny Edges"
[image5]: ./examples/image5.jpg "Hough Transform"
[image6]: ./examples/image6.jpg "Final Image"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps. 

- First, I converted the images to grayscale. This I did using the helper function grayscale(image).
- Second, I did a Gaussian Blur with a kernel size of 5, using the helper function gaussian_blur(gray_image, kernel_size)
- Third, I used canny edge detection with a low threshold of 100 and high threshold of 150 to detect the outline edges
- Fourth, I identify the region of interest with some trial and error. this is the region with a high likely hood of containing the current lane.  This for me is in the range of [(480,310),(500, 310), (895,539), (80, 539)]
- Fifth, I use Hough Trasform to detect lines with in the region of interest. The arguments used are rho = 1, theta = np.pi/180, 25, min_line_len = 5 & max_line_gap = 150
- Sixth, I merge the orginal image with the image containing identified lane lines, to come up with a combined image

The output corresponding to each step in the pipeline for the test file test_images/solidWhiteRight. is shown below

#### Step-1
![alt text][image1]

#### Step-2
![alt text][image2]

#### Step-3
![alt text][image3]

#### Step-5
![alt text][image5]

#### Step-6
![alt text][image6]




In order to draw a single line on the left and right lanes, I modified the draw_lines() as follows:
- Collect all the lines identified by Hough Transform on the region of interest
- For each line for the Hough Transfrom identify the slope and intercept using the (x1,y1) - (x2,y2) pairs of the line
- If the slope is less than zero, identify it as a line segment within the left lane. Else it is identified as part of the right lane
- Find the average of slopes & intercepts collected for all the right line segments
- Start of the lane marker will be at bottom of the image. The end of the lane marker will be at 75% of the image height. Fixing these will help determine the y coordinates for all our lane marker end points
- Use the average slope, average intercept and the Y Coordinates, to compute the X-Coordinates of the lane marker end points
- Use cv2.line to draw lines using the computed endpoint coordinates.



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane is along a curved path. The current method does not perform very well on curves

The region of interest is configured for this specific camera view. It may not work very well if the view is adjusted for a different camera position or angle.

We have not tested it on darker situations line night drives or dimly lit roads. These could be a challenge for the existing code and logic


### 3. Suggest possible improvements to your pipeline

A constantly aggregated slope computation taking into account previous frames may resolve the difficulty in navigating curves

A way to compute the region of interest in a dynamic manner by determining the camera location and end of hood

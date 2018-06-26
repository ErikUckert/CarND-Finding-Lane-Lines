# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./pipeline_images/hsv_image.png "HSV Image"
[image2]: ./pipeline_images/yellow_masked_hsv_image.png "Yellow Masked Image"
[image3]: ./pipeline_images/white_masked_hsv_image.png "White Masked Image"
[image4]: ./pipeline_images/combined_image.png "Combined Image"
[image5]: ./pipeline_images/masked_image.png "region masked Image"
[image6]: ./pipeline_images/blurred_image.png "blurred Image"
[image7]: ./pipeline_images/canny_image.png "canny Image"
[image8]: ./pipeline_images/hough_lined_image.png "hough line Image"
[image9]: ./pipeline_images/weighted_image.png "final Image"
---

## Changelog
v.1.0 - Initial Version
v.2.0 - Adapted Version for drawing solid lines throughout most of the image material


## Reflection

### 1. At first I will describe my pipeline and explain how I modified the draw_lines() function for better results at the challenge video stream.

The Algorithm to perform a lane line detection on images and video stream data consists of two main elements: Helperfunctions and a image preparation and analysis pipeline.

My pipeline consisted of 2 steps. A image preparation step an the actual edge lane line detection and drawing. In **Step ONE**, I converted the images to hsv colorspace to seperate white and yellow colors in the images. After that I set a region of interesst (4 sided polygon) for masking the relevant image areas, where i expect lane lines. At the end i proceed with a gaussian blurring to refine the image for edge detection.

In **Step TWO** I perform the actual edge detection and drawing. This step consists of 3 mayor parts. First i detect the lines with the hough line function and after this step i average the detected lines and draw them into the image material. For the actual averaging i adapted code from this source: https://medium.com/@mrhwick/simple-lane-detection-with-opencv-bfeb6ae54ec0
which provides an other notable approach for solving the lane detection problem.
 
**Here are some images to show how the pipeline works:**


_Converting image to HSV Colorspace_

![alt text][image1]


_Masking yellow colors in the image_

![alt text][image2] 

_Masking white colors in the image_

![alt text][image3]

_Combine the two color masks in one image_

![alt text][image4]

_Masking a region of interesst in the image_

![alt text][image5] 

_blurring the image_

![alt text][image6] 

_detect edges in the region of interest_

![alt text][image7] 

_draw hough lines out of the canny edges_

![alt text][image8] 

_add the hough lines to the original image_

![alt text][image9] 

### 2. Potential shortcomings with my current pipeline

The mayor shortcoming of the lane line detection pipeline is the variance of the image stream scaling. Lines are filtered by their scope, so whenever a different camera angle is used, and / or the scopes of the detected lines are getting more steep or flat, there is a reasonable chance of filtering out the actual lane lines.

Another shortcoming could be the image quality. Certain dark spots or a changing road surface can cause false lane lines. Driving curves isn´t well displayed because the drawed lines are straight lines.


### 3. Possible improvements to the pipeline and helper functions

A possible improvement would be to implement a better filter algorithm to improve the filtering of what is potentialy not a lane line.

Another potential improvement could be to draw shortes lines to display a curvy road more accurate.

# **Finding Lane Lines on the Road** 

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

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

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project I will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images. I did this during my time at the [![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive).

Running this Project
---

**Step 1**  -- Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7).

**Step 2** -- Open the code in a Jupyter Notebook

This project is writen in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an Ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. 

**Step 3** -- Run the code

To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  There you can execute the code stepwise as you like.


Reflection
---

At first I will describe my pipeline and explain how I modified the draw_lines() function for better results at the challenge video stream.

The Algorithm to perform a lane line detection on images and video stream data consists of two main elements: Helperfunctions and a image preparation and analysis pipeline.

My pipeline consisted of 2 steps. A image preparation step an the actual edge lane line detection and drawing. In **Step ONE**, I converted the images to hsv colorspace to seperate white and yellow colors in the images. After that I set a region of interesst (4 sided polygon) for masking the relevant image areas, where I expect lane lines. At the end I proceed with a gaussian blurring to refine the image for edge detection.

In **Step TWO** I perform the actual edge detection and drawing. This step consists of three mayor parts. First I detect the lines with the hough line function and after this step I average the detected lines and draw them into the image material. For the actual averaging I adapted code from this source: https://medium.com/@mrhwick/simple-lane-detection-with-opencv-bfeb6ae54ec0
which provides an other notable approach for solving the lane detection problem.
 
**Here are some images to show stepwise how the pipeline works:**


_1 Converting image to HSV Colorspace_

![alt text][image1]


_2 Masking yellow colors in the image_

![alt text][image2] 

_3 Masking white colors in the image_

![alt text][image3]

_4 Combine the two color masks in one image_

![alt text][image4]

_5 Masking a region of interesst in the image_

![alt text][image5] 

_6 blurring the image_

![alt text][image6] 

_7 detect edges in the region of interest_

![alt text][image7] 

_8 draw hough lines out of the canny edges_

![alt text][image8] 

_9 add the hough lines to the original image_

![alt text][image9] 

Potential shortcomings with my current pipeline
---

The mayor shortcoming of the lane line detection pipeline is the variance of the image stream scaling. Lines are filtered by their scope, so whenever a different camera angle is used, and / or the scopes of the detected lines are getting more steep or flat, there is a reasonable chance of filtering out the actual lane lines.

Another shortcoming could be the image quality. Certain dark spots or a changing road surface can cause false lane lines. Driving curves isn´t well displayed because the drawed lines are straight lines.


Possible improvements to the pipeline and helper functions
---

A possible improvement would be to implement a better filter algorithm to improve the filtering of what is potentialy not a lane line.

Another potential improvement could be to draw shortes lines to display a curvy road more accurate.


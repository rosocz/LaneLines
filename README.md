# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md 

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)


# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./image_output/segment_output.png "Segment lines"
[image2]: ./image_output/points_to_line.png "Points to line by linear regression"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

First, I converted images to grayscale, then I implemented Gaussian blur and used canny method 
to find edges. Last step of preprocessing preparation is cut out relevant polynom.

When the image has only relevant edges and rest of the space is black, Hough transformation finds lines in 
a group of points. Combining original image and indentified lines ploted in red, 
we get first version of line detection where we have every detected lane line surrounded by red line.

![alt text][image1]

Next step is to draw single line over detected lines. We can see detected lines 
as a group of start-end points and categorize them to left and right group based on line parameters they are
part of. Linear regression of all relevant points creates single line. Function polyfit from numpy was add 
to function `draw_lines()`.

![alt text][image2]

*Image 2: Here you can see green points as the input and red lines as the outcome*

These all steps work for video as well, all process just iterates throught all images in video.

Last part was solving Optional Challenge. All steps are still the same only the group of points used 
to count linear regression is taken from all images already processed. With help of points from already 
processed images we can find line even at images where line detection is not easy.


### 2. Identify potential shortcomings with your current pipeline

In fact any fixed definition of values is a potential problem. We define parameters for canny method and hough 
transformation as fixed values but we are working with video, where conditions are changing in time.

Next known problem occures when we get significant part of the road where line detection is not possible. 
Our line starts to be very inaccurate because points used to count linear regression are not relevant anymore.

Another problem could occure when we get sharp turn and one of the lines crosses middle of the image. I assume 
that the image is split into right and left part and both parts contain one line.

### 3. Suggest possible improvements to your pipeline

Parameters for edge detection and finding lines could be set automatically to take into account specific conditions 
of image.

The way how we decide if point belongs to the left or right line could be improved by automatic finding border 
between lines.


The Project
---

## If you have already installed the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) you should be good to go!   If not, you should install the starter kit to get started on this project. ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook


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

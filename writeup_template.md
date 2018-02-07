# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 
First, I converted images to grayscale, then I implemented Gaussian blur, kernel size 11 and used canny method 
to find edges. Last step of preprocessing preparation is cut off relevant polynom.

When I have image where only relevant edges are present and rest of the space is black, Hough transformation
 helps to find lines in a group of points. To avoid detecting clearly wrong lines I created function, 
which checks angle between each line and horizontal axis and line's slope.
Combining original image and indentified lines ploted in red, we get first version of line detection where we 
have every detected lane line surrounded by red line ploted.

Next step is to draw just single line over detected lines. I took detected lines as a group of start-end points 
and based lines parameters I categorized point to left and right group and than I use linear regression to get 
single line.

These all steps work for video as well, all process just iterates throught all images in video.

Last part was to solve Optional Challenge. All steps are still the same only the group of points used 
to count lineat regression is taken from all images already processed. With help of points from already 
processed images we can find line even at images where line detection is not easy.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

# **Finding Lane Lines on the Road** 

### Introduction

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Use the tools in the Udacity lessons to identify lane lines on the road
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:

* First, I converted the images to grayscale.
* Then I applied Gaussian smoothing using the`cv2.GaussianBlur` function
* As lanes on the road usually consist of linear lines, we use the Canny Edge Detection algorithm to detect edges in the picture.
* Fourth, we use region select, assuming that the front facing camera that took the image is mounted in a fixed position on the car, such that the lane lines will always appear in the same general region of the image. This will help use detect the lanes for the car we are driving. 
* Next, we use the Hough Transform to find the lanes in the selected region.
* Then, I draw the detected lines and superimpose them with a red color on our original image using the `weighted_img` function.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

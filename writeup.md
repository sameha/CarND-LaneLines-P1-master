# **Finding Lane Lines on the Road** 

### Introduction

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Use the tools in the Udacity lessons to identify lane lines on the road
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: './examples/writeup_image1.png' "Original Image"
[image2]: './examples/writeup_image2.png' "Grayscale Image"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps, starting with a colored image of the road like this:

![alt text][image1]

We perform the following steps:

1- First, we convert the images to grayscale:

![alt text][image2]

2- Then I applied **Gaussian Smoothing** using the`cv2.GaussianBlur` function:

3- As lanes on the road usually consist of linear lines, we use the Canny Edge Detection algorithm to detect edges in the picture.
4- Fourth, we use region select, assuming that the front facing camera that took the image is mounted in a fixed position on the car, such that the lane lines will always appear in the same general region of the image. This will help use detect the lanes for the car we are driving. 
5- Next, we use the **Hough Transform** to find the lanes in the selected region. Note that the `hough_lines` functions used calls a special function to draw the lines, `draw_lines()`. More on that later.
6- Finally, I draw the detected lines and superimpose them with a red color on our original image using the `weighted_img` function.

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

# **Finding Lane Lines on the Road** 

### Introduction

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Use the tools in the Udacity lessons to identify lane lines on the road
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/writeup_image1.png "Original Image"
[image2]: ./examples/writeup_image2.png "Grayscale Image"
[image3]: ./examples/writeup_image3.png "Gaussian Smoothing"
[image4]: ./examples/writeup_image4.png "Canny Edge Detection"
[image5]: ./examples/writeup_image5.png "Region Selection"
[image6]: ./examples/writeup_image6.png "Hough Lines"
[image7]: ./examples/writeup_image7.png "Final Output"
[image8]: ./examples/writeup_image8.png "Improved Draw Lines"
[image9]: ./examples/writeup_image9.png "Improved Final Output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps, starting with a colored image of the road like this:

![alt text][image1]

We perform the following steps:

1- First, we convert the images to grayscale:

![alt text][image2]

2- Then I applied **Gaussian Smoothing** using the`cv2.GaussianBlur` function:

![alt text][image3]

3- As lanes on the road usually consist of linear lines, we use the Canny Edge Detection algorithm to detect edges in the picture:

![alt text][image4]

4- Fourth, we use region select, assuming that the front facing camera that took the image is mounted in a fixed position on the car, such that the lane lines will always appear in the same general region of the image. This will help use detect the lanes for the car we are driving:

![alt text][image5]

5- Next, we use the **Hough Transform** to find the lanes in the selected region. Note that the `hough_lines` functions used calls a special function to draw the lines, `draw_lines()` (More on that later):

![alt text][image6]

6- Finally, I draw the detected lines and superimpose them with a red color on our original image using the `weighted_img` function:

![alt text][image7]

In order to draw a single line on the left and right lanes, I modified the original `draw_lines()` function by:

* Find the Center Cooridinates of the image to seperate left and right lines

* Find X and Y coordinates of left and right lanes. If the line has a negative slope and is on the left side of the image, we consider it as a left lane. If the line has a positive slope and is on the right side of the image, we consider it as a right lane.

* Using the left and right line segments, we use the `np.polyfit` function to find the slope (`m`) and intercept (`b`) of the full exteneded line.

* Next, we use our selected region to extrapolate to the top and bottom of the lane:

![alt text][image8]

* The final improved output is shown below:

![alt text][image9]



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lanes are not relatively in the center of the image, but to the corners of the image.

Another shortcoming could be when there is a steep curve like the challenge video.


### 3. Suggest possible improvements to your pipeline

In cases of steep curves, a possible improvement would be to seperate the extended line into two lines.

Another potential improvement could be to recalculate the slope of the extended line based on the current line and previous lines (take history into consideration).

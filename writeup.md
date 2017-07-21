# **Finding Lane Lines on the Road** 

## My project report for the Project 1 of Self Driving Car Nanodegree term 1.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "Solid White Right"

---

### Reflection

### 1. Image processing pipeline

At first, I make my pipeline as below
- **Step1:** convert image to grayscale
- **Step2:** apply gaussian blur to grayscale image
- **Step3:** use canny function to find edges from the image
- **Step4:** set region of interest to avoid detection of useless lines
- **Step5:** by using Hough Transform, try to get coordinations of lines
- **Step6:** draw lines with coordinations from Step 5
- **Step7:** display lines on the original image

In this pipeline, I try to find optimal parameters of some functions like gaussian blur, canny, hough line by trial and error. 
It is enough for test images. The result of my pipeline for image is shown below.

![][image1]

In the case of video, the output lines are busy to move and jump.
So I modify the default draw_lines() function by using average of slopes and lines of past frames.




------------
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

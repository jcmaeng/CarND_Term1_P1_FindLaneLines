# **Finding Lane Lines on the Road** 

## My project report for the Project 1 of Self Driving Car Nanodegree term 1.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "Solid White Right"
[image2]: http://akash0x53.github.io/images/norm/eq.png "RGB Normalization Equation"

---

### Reflection

### 1. Image processing pipeline

At first, I make my pipeline as below

**(My first pipeline)**
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

At the first time, I want to draw solid lines with segmented lines.
So I modified the default draw_lines() function with slope values.

Slope value is calculated by the equation. (x1, y1) and (x2, y2) are each end point of a line.

* Slope = (y2 - y1)/(x2 - x1)

Since (0,0) is in the upper left corner, I think that if slope value is positive, the line is along the right lane.
In the same manner, if slope value is negative, the line may be the part of left lane.
I gathered slope values of each lines along the side and take mean value of each lane line.
Along the region of interest, I could compute coordinates of each lane lines with slope equation.
y1 and y2 is fixed because of the region of interest, I just compute x1 and x2 like belows

* x1 = -(y2-y1)/mean_of_slopes + x2
* x2 = (y2-y1)/mean_of_slopes - x1

After obtaining each coordinates, I could draw the solid lines of lane on the images.

In the case of video, the output lines are busy to move and jump.
So I try to use the information of past frames.
Use the average of mean slope value in each frame to smooth the move of lines in videos.
The latest information should affect the result with same ratio, I just used 10 past frames for smoothing.

Lastly, I tried to apply my pipeline to the challenge video, but it did not work properly.
The video is larger than previous. And some images in the video are too bright and has complex lines.
To obtain proper lines, I adjusted the region of interest and use the color image instead of grayscale.
Then normalize the image with below eqation from [akash](http://akash0x53.github.io/blog/2013/04/29/RGB-Normalization/ "AKASH's blog").

![][image2]

Finally, I could make the pipeline for the challenge video.

**(Pipeline for challenge video)**
- **Step1:** normalize image with RGB normalization
- **Step2:** apply gaussian blur to grayscale image
- **Step3:** use canny function to find edges from the image
- **Step4:** set region of interest to avoid detection of useless lines
- **Step5:** by using Hough Transform, try to get coordinations of lines
- **Step6:** draw lines with coordinations from Step 5
- **Step7:** display lines on the original image

You can see the result of my work in my jupyter notebook files shared in my GitHub ([mygithub](https://github.com/jcmaeng/CarND_Term1_P1_FindLaneLines "here"))


### 2. Identify potential shortcomings with your current pipeline

As I think, potential shortcomings with my current pipeline is as follows.

- There is no automated way to find optimal parameters for the image processing functions. (Canny, Hough Lines, Region of Interest, etc)
- The pipeline may not cover the various situations such as obstacles on the lane line, rainy day, and so on.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use various color space to detect correct lane lines.
I think that this may help to recognize lane lines in various environment conditions.

Another potential improvement could be to use the accumulated data of various conditions like machine learning.

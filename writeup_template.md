# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidYellowCurve_with_lane_markings.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps. 
Step 1: The image is converted to grayscale for further processing.
Step 2: We apply a gaussian filter for smoothing and noise removal to the grayscale image, the chosen kernel for this step is 5x5. 
Step 3: The next step we apply the canny edge detector to detect the edges in our image. The parameters set for the canny detectors are the high and low thresholds, the filter size was left to the default 5x5.
Step 4: From the previous step multiple edges (changes in the image) were detected, we now modify our region of interest relying on visual inspection. We hence, blackout any pixels which are outside our region of interest.
Step 5: we know try to map the edge points to hough lines using the hough transform and finally draw the lines to the original image. Multiple tunable parameters exist for this step such as the grid precision represented by rho and theta and other features belonging to the detecting line such as the maximum gap interms of pixels or the line length.

In steps 2-5 different values of the parameters have been tried out to come up with the best possible result. Choice of the parameters were based on visual inspection. 

An example of the detected lanes on one of the test images is shown below


![alt text][image1]

One main task was to modify the draw lines function which was primarly outputing individual detected line segments to continuous lines representing the lanes. In order to do that the adopted approach was as follows:
1- Compute the slopes for each line to decide whether it belongs to the right or left lane (right lanes have +ve slopes while left ones have -ve slopes)
2- Aggregate all lines coordinates in lists x1,y1,x2,y2 per lane.
3- Average the points (for robustness of the line) and compute the slope.
4- substitute in the calculated slope with y1=image bottom and y2=y2 of last detected line in the lane and compute the corresponding x1 and x2.
5- Finally plot the detected lines 


### 2. Identify potential shortcomings with your current pipeline

The potential shortcomings are:
1- The hough transform method used is tailored to line detection in case of roads with high curvature (as in the challenge video) the method fails to detect the lane markings.
2- The choice of parameters is done by inputing different parameters to the pipeline and visually checking the quality of the produced output, this could be quite exhaustive if we want to try many parameter combinations.



### 3. Suggest possible improvements to your pipeline

Possible improvements would be:
1 - For lane markings detection use another method which is more general than hough lines transform which and capable of detecting arbitary shapes. Generalized hough transform could be one possibility.
2 - For parameters choice a GUI tool could be created to ease the choice of the parameters.


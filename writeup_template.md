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
[image2]: Week-1.jpg "Processing Pipeline"
[image3]: ./results/solidWhiteCurve.jpg "Draw Lines"
[image4]: ./results_stabilized/solidWhiteCurve.jpg "Lane Identification"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

#### Overview
The processing pipeline has the following stages. 
![alt text][image2]

#### Lane Identification
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by grouping the slopes of the lines identified by the Hough lines function. The slope of the line segment also indicates 
if the lane line is the left or the right lane. This resulted in images like the one below.
![alt text][image3]

#### Lane Extrapolation
To extrapolate the lines, the equation `y = mx + c` was used. The rationale was that the dashed lines would have the same slope or `m`. To filter out spurious results the following steps were taken.
* Eliminate lines with slope between `0.45` and `-0.45`. This ensured that the more horizontal lines are eliminated
* Eliminate outliers (where difference with mean is > twice the standard dev). This was done for both `m` and `c`. 

The result is as shown below. 
![alt text][image4]

#### Lane Stabilization
Applying the lane extrapolation on video resulted in a jittery line which was also heavily dependent on frame data. This resulted in the challenge video having lines which were all over the place at time. To fix this, an average 
slope and intercept for the left and right lane (over 10 frames) was adopted. This resulted in a much more stable and robust lane identification. The challenge was to identify the starting slopes and intercepts, especially if 
the starting frame had spurious data (in the form of Hough lines). Hence the first 9 frames are not considered for averaging.

### 2. Identify potential shortcomings with your current pipeline

1. The current red is drawn as a straight line - this may not be a good idea for turns (especially tight ones)
2. Too many loops
3. Lots of magic numbers in code (slopes, thresholds, ROIs)
4. The averaging is currently over 10 frames.
5. Not tested what happens during lane changes, and when used on roads with no lane markings. 


### 3. Suggest possible improvements to your pipeline
1. Improve the line to handle curves - maybe a set of points joined by a spline curve? What is the maximum curve the approach can handle?
2. Reduce loops and improve performance
3. Parameterize magic numbers 
4. Handle lane changes, roads with no lane markings 

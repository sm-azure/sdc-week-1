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
[image2]: .Week-1.jpg "Processing Pipeline"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline has the following stages. 
![alt text][image2]



In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


1. The current red is drawn as a straight line - this may not be a good idea for turns (especially tight ones). Maybe a set of points joined by a spline curve?
2. Too many loops
3. Lots of magic numbers in code (slopes, thresholds, ROIs). Has to be parameterized 
4. The averaging is currently over 10 frames. This results in slow changes when lane lines change rapidly.


### 3. Suggest possible improvements to your pipeline


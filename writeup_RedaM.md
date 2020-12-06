# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:
1-First, I converted the images to grayscale.

[Grayscale]: [./test_images_output/solidWhiteCurve_gray.jpg]

2-Applied guassian filter.
[Guassian Filter]: [./test_images_output/solidWhiteCurve_blur.jpg]

3-Using canny edges to detect all transition in gray scale to detect all lines.
[Canny edges]: [./test_images_output/solidWhiteCurve_edge.jpg]

4-Add a filter region ( Taking into account the hood area in challenge video)
[Mask Applied]: [./test_images_output/solidWhiteCurve_masked_edge.jpg]

5- Apply Hough transform to populate lines that are supposed to be one line, but also make sure to filter all lines that are out of slope expected for left and right lanes to avoid detecting the horozontal lines as part of the lanes (issue faced in second video).
[Hough transform]: [./test_images_output/solidWhiteCurve_Hough.jpg]

6- Final image after merging the line into the original image
[Final image]: [./test_images_output/weighted_img.jpg] 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by the following:
1-Looping over all the lines got from Hough transofrm to allocate which ones are from left lane and which ones are from right lane
2-For each line point group we run the polyfit to detec the line equation both slope and intercept 
3-Filter on lines that has slope more or less than threshould.
4-Get mean value for x points and for y points (left and right) to get the line equation which best describes the lane
5-Start drawing left/right lanes only if we have points 
6-Lane will alway start from end of screen (max y) 
 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is a curve lane like the challenge section, where I think needed to have a different way of drawing the lane instead of straight line we needed to have an equation to draw it as a part of larger circle 

Another shortcoming could be when lanes doesn't have much different color than the actual pavement which will lead to the lane markings to be missed.


### 3. Suggest possible improvements to your pipeline

First improvement (tried but didn't succeed), is to add a step in the pipline to use the HSV domain to filter on any lane that has a color range of whites or Yellows, and then color this part with more visble line color (Red for ex) before doing the first step of RBG2GRAY 

Second improvement, would be changing the Lane drawings from line equation to be something with curve such as sin(x), where we 
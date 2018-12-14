# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve.jpg "Before"
[image2]: ./test_images_out/solidWhiteCurve.jpg "After"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of below steps. 
1. Convert image to grayscale
2. Apply gaussian blur to smooth the image
3. Canny edge detection with threshold low: 50, high: 150
4. Filter a quadrilateral shape where the lanes are present as masked edges
5. Apply hough transform by adjust inputs but mostly threshold, minimum line length and max gap between lines
6. Apply the hough transformed output over copy of original image to get red lines

![alt text][image1] ![alt text][image2]

For the **draw_lines()** function, I used the approach which can be summarized as averageing, extrapolation and fallback on failure. Initially I also did one more simplified approach of just taking the extreme points and joining them. Later I refined it with average of the points before connecting and then extrapolating them from the base of the image frame till the middle of the image (which is the farthest sight of camera till straight lane lines are visible). Before averaging I try to separate the lines into left & right lane depending on the slope of the segments but sometimes I couldn't detect any line on left or right, in that case I used the fallback approach to draw the hough lines. 


### 2. Identify potential shortcomings with your current pipeline

I would have liked to get that thick line going but my lines are thin. Of course when road is curved like in the challenge, the lane detection goes haywire. The averaging of lane lines could be better but I think it can be improved easily if I had more knowledge of the python libraries that deal with these features with inbuilt methods. I also think the parameters for Canny and Hough transform steps can be better because it was hit & trial observation. I would have appreciated it more if we knew how to detect these parameters with certainity. I felt I spent a lot of time on parameters which I didn't like.


### 3. Suggest possible improvements to your pipeline

Better parameters for Canny and Hough transforms. Better line averaging methods. Thicker lines post extrapolation (modifying the thickness parameter in draw_lines() didn't had much effect IMO). 

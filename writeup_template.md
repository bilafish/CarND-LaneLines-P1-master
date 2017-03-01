#**Finding Lane Lines on the Road** 

##Writeup


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied Gaussian smoothing to reduce noise. Next, Canny is used to detect the strong edges in the image. Region masking is then used to mask the additional edges detected in the image that does not correspond to lane lines by assuming that the camera is always centred in the lane and in the middle of the car. Finally, I used Hough transform to detect line segments that correspond to the lane lanes and drew the lane lines by fitting detected line segments linearly and extrapolating the line towards the bottom of the image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by including conditions to sort the line segments according to gradient into two buckets: one for each side of the lane. A linear regression is used to obtain the m and b values which allows us to calculate the x value assuming that the y value is the height of the image (obtained from im.shape). Therefore, this will ensure that the lane lines will be drawn to a point along the bottom axis of the image by extrapolation.

These are some of the lane lines detected from my test image set:
<img src="/test_images/solidWhiteCurve.jpg-test.jpg"/>
<img src="/test_images/solidYellowCurve.jpg-test.jpg"/>
<img src="/test_images/solidYellowLeft.jpg-test.jpg"/>
<img src="/test_images/whiteCarLaneSwitch.jpg-test.jpg"/>


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the camera or the car is not well-centered in the lane. This might cause the lanes to fall out of the masked region.

Another shortcoming could be that the draw_lines() function is unable to model curved lane lines.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to include x-coordinate filtering in the draw_lines() function to reduce chance of misclassification of lane lines detected and drawn.

Another potential improvement could be to optimise the Hough Transform parameters for better lane line detection such as curved lines.

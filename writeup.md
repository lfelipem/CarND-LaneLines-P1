**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline is done in a function called processImage, which receives a image (original frame) as parameter and return a final frame including the original image and the over position line marks. 
In this function is done a gaussing smoothing followed by a Canny Transform to find the image edges. Next step, a polygon is defined and applied as mask into the image, resulting in a image with edges only in the area of interest.
The Hough Transform (hough_lines) is applied to identify lines following its parameters. The function draw_lines, which is called inside hough_lines, was modified to analysis each line from hough_lines and select the best match to be left and right lane line.
This is done first by grouping lines by slope, slope<-0.3 are left and slope>0.3 are right, lines with slopes between this range are discarded.
Then, the longer line from each group is selected to be extrapolated, using the slope and intercept from the selected line, Xs coordinates are calculated for Y at the bottom of the frame and to Y at 3/5 of the height.
One last function, called averageLines, was used to try to solve the flickering issue. This function uses the last 10 positions of each coordinate, as a moving average, to try to filter the high frequency oscilation.

[image1]: ./test_images_out/solidWhiteCurve.jpg "solidWhiteCurve"
[image1]: ./test_images_out/solidWhiteRight.jpg "solidWhiteRight"
[image1]: ./test_images_out/solidYellowCurve.jpg "solidYellowCurve"
[image1]: ./test_images_out/solidYellowCurve2.jpg "solidYellowCurve2"
[image1]: ./test_images_out/solidYellowLeft.jpg "solidYellowLeft"
[image1]: ./test_images_out/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch"



###2. Identify potential shortcomings with your current pipeline

Potentials shortcoming: 
Night images would be very difficult to identify.
Very curvilinear roads would have lanes out of the polygon area, which would be ignored.
Any inclined road would limited the camera view of the lanes.
Roads without lane marks.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to improve stability of the lane marks. The average technique gave a little improvement but its not perfect.
Solve the first frame marks lane error from the challenge video.



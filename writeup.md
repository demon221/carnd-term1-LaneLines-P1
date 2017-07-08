**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "ImageWithLanes"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps.

1. The images are converted to grayscale.

2. Using Gaussian filter with kernel 5.

3. Detected edges using Canny algorithm. Threshold values are calculated using the median of pixel intensities.

4. Define a four sided polygon ROI to mask the image edges.

5. Detected all possible lines using Hough Transform algorithm and draw red lines on the images.

6. Then in order to draw a single line on the left and right lanes, I modified the draw_lines() including following steps:

- Distinguish right lanes and left lanes based on the slope of Hough Transform output lines.  Lines with the negative slope are left lane line candidates. Lines with positive slope are right lane line candidates.
- Wipe off the lines with abnormal high or low values of slope. Only lines which absolute slope in the range of 0.5~2 are reserved.
- Calculate the mean value of slope and interception of each side of candidates lines.
- Extrapolate both lan lines to the bottom of a image and to the lowest y-axle value point.
- Draw the two lanes to the initial images.

The images after lanes detection are looked like this.

![alt text][image1]







### 2. Identify potential shortcomings with your current pipeline


1. The robustness of this lane detection pipeline will get worse when the edges between roads and lanes is not clear or contrast is weak.
2. During the switch of shadow and sunlight, outcomes of hough transform will have much noise which may cause to wrong detection.
3. Region of interest is now constant region, when the car is changing lanes this pipeline will no longer be workable.
4. Most parameters are constant and not self adaptive.


### 3. Suggest possible improvements to your pipeline

1. For switch of shadow and sunlight, a histogram adaption may be useful.
2. Color selection can be used to improve the accuracy of lane detection.
3. Parameters of Canny and Hough can be improved for self adaptive.
4. Method of Deeplearning can let the algorithm much more robust.

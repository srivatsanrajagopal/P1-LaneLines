
# Finding Lane Lines on the Road

Udacity CarND Nanodegree problem
The goals / steps of this project are the following:

Make a pipeline that finds lane lines on the road
Reflect on your work in a written report
Reflection

## 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The five steps used in the pipeline are:
1. Convert the color image to Gray scale 
2. Apply Guassian Blur to reduce noise in the picture. I used a kernel value of 9 for masking
3. Apply Canny Edge detection to identify the interesting edge pixels. I used a 1:3 ratio for the threshold.
4. I outlined the region of interest as the lane on which the car was driving on and masked out everything else
5. I used the Polar coordinate based Hough Transform to identify the groups of lines through the pixels in the region of interest.
 
## In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

I followed the following steps to extrapolate the left and right lane lines:
1. I grouped the smaller lines into the left and right lane line buckets by their slopes (positive vs negative)
2. For each bucket I calculated the mean slope and mean intercept which formed the parameters for the new single line which would replace the collection of lines in the bucket
3. To reduce the "jump" in this single new line across frames,  I averaged the full line with the previous lines. This gave a much smoother line rendering across frames in a video stream.

Testing the pipeline on the images:


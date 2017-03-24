
# Finding Lane Lines on the Road

Udacity CarND Nanodegree problem

This repository contains the first project deliverables.

* Image outputs with lane lines marked for the test images provided in the poject are in [test_images_output directory](CarND-LaneLines-P1/test_images_output)
* Video outputs for the first two input files is in [test_videos_output](CarND-LaneLines-P1/test_videos_output)
* The optional Challenger video is still not solved. Will continue working on it.

## The Pipeline for identifying lane lines

The five steps used in the pipeline are:
1. Convert the color image to Gray scale 

![Alt text](CarND-LaneLines-P1/test_images_output/grayscale_example.png?raw=true "Gaussian Blur")

2. Apply Guassian Blur to reduce noise in the picture. I used a kernel value of 9 for masking
![Alt text](CarND-LaneLines-P1/test_images_output/gaussian_blur_example.png?raw=true "Gaussian Blur")

3. Apply Canny Edge detection to identify the interesting edge pixels. I used a 1:3 ratio for the threshold.
![Alt text](CarND-LaneLines-P1/test_images_output/canny_edge_example.png?raw=true "Canny Edge")

4. I outlined the region of interest as the lane on which the car was driving on and masked out everything else
![Alt text](CarND-LaneLines-P1/test_images_output/masked_edges_example.png?raw=true "Canny Edge")

5. I used the Polar coordinate based Hough Transform to identify the groups of lines through the pixels in the region of interest. I then applied Extrapolation technique as below to draw a single smooth line through the hough transform lines.
 ![Alt text](CarND-LaneLines-P1/test_images_output/hough_lines_masked_example.png?raw=true "Extrapolated Hough Line")


## Extrapolated Lane line from muliple Hough Transform lines

I followed the following steps to extrapolate the left and right lane lines:
1. I grouped the smaller lines into the left and right lane line buckets by their slopes (positive vs negative)
2. For each bucket I calculated the mean slope and mean intercept which formed the parameters for the new single line which would replace the collection of lines in the bucket
3. To reduce the "jump" in this single new line across frames,  I averaged the full line with the previous lines. This gave a much smoother line rendering across frames in a video stream.

This resuls in the final image where the lane lines are transposed over the original image:
 ![Alt text](CarND-LaneLines-P1/test_images_output/whiteCarLaneSwitch.jpg?raw=true "Final Combo image")




# Self-Driving Car Engineer Nanodegree


## Project: **Finding Lane Lines on the Road** 
***
In this project, the goal is identify lane lines on the road using the tools we have learned. These tools include color selection, region of interest selection, grayscaling, Gaussian smoothing, Canny Edge Detection and Hough Tranform line detection.

## Reflection

My lane detection pipeline consisted of six steps to process an image and detect the lanes in that image.

### Pipeline Description

The first step is to convert the input image into grayscale.

The second step is to apply a gaussian_blur (gaussian smoothing) to the grayscale image to reduce the noise in the image.

The third step is to identify the boundaries of the objects in the image via canny edge detection.

The fourth step is to identify and apply a mask for the region of interest for lane detection.

The fifth step is to apply a hough transform to the masked image to identify the lines (lanes) formed by the canny edges. Following this transformation, the equation for those lines are identified by the draw_lines function. 

I modified the draw_lines function to seperare the x and y coordinates of the lines identified by the hough transform by calculating the slopes ((y2-y1)/(x2-x1)). Positive slopes with magnitudes higher than the threshold are identified as left lane coordinates, while negative slopes with magnitudes lower than the threshold are identified as right lane coordinates. The average slope and x,y coordinates are calculated and then used to determine the best x coordinates for the average line. The final result is then plotted on a blank image.

The sixth and final step is to combine the input image and processed image with drawn lines. This is done by adding the weighted versions of these images together to achieve the final overlaid image with lane detections.

### Shortcomings and Suggestions

Although the results are adequate for solidWhiteRight.mp4 and solidYellowLeft.mp4, the pipeline does not work well on challenge.mp4. This is indicative that the pipeline may not be robust enough to function on input with different asphalt colors, lighting conditions and inconsistent shadows. That is, despite the region of interest mask, there is enough noise to introduce large errors to the lane detection. Furthermore, the draw_lines function determines straight lines, whereas, challenge.mp4 consists of a continously turning lane, however, not enough to be the sole contributor to the error.

As a result, possible future improvements might be different more accurate image processing techniques that would better identify lanes, such as processing in different color spaces. Furthermore, the draw_lines function might be modified to produce curved lines by fitting to a polynomial equation.

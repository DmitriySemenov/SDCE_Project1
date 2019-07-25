# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Make the lines continuous 
* Apply it to images first, then to videos
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./writeup_images/colormasked.jpg "Color Masked"
[image2]: ./writeup_images/gray.jpg "Grayscaled"
[image3]: ./writeup_images/blurred.jpg "Blurred"
[image4]: ./writeup_images/edges.jpg "Canny Edges"
[image5]: ./writeup_images/masked.jpg "Region Of Interest"
[image6]: ./writeup_images/final.jpg "Final Result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.


My final pipeline consisted of 8 steps (not including loading and saving an image).
The steps are the following:
    0. Load image
    1. Convert image from RGB to HSV color space
    2. Using HSV, find yellow and white masks and apply to RGB image to only leave yellow and white colors
    ![alt text][image1]
    3. Convert RGB to grayscale
    ![alt text][image2]
    4. Apply Gaussian blur to grayscale image
    ![alt text][image3]
    5. Perform Canny edge detection using blurred image
    ![alt text][image4]
    6. Define a region of interest and mask away the undesired portions of the image
    ![alt text][image5]
    7. Retrieve Hough lines from the region of interest part of the image
    8. Apply lines to the original image
    ![alt text][image6]
    9. Save image with applied lines

Initially, pipline included only 6 steps as I didn't have steps 1 and 2 and started straight with converting RGB to grayscale.
However, optional challenge video made me reconsider my approach and include those two steps.
They help ignore some of the incorrectly detected lines due to tree shadow and road imperfections.

In order to draw a single line on the left and right lanes, I had to modify the draw_lines() function.


### 2. Identify potential shortcomings with your current pipeline

Some of the shortcomings with the current pipeline:

The lines are a bit jittery because the final line is calculated using the averaging of all the found Hough lines and those are not always perfect.
Detection of lines is parameter sensitive and may not work well given different lighting conditions (as challenge video highlighted before color detection was added).


### 3. Suggest possible improvements to your pipeline

Possible pipeline improvements would be:

1) Adding global variables to track previously detected lanes. 
This would allow to smooth out the lanes as the frame-to-frame changes in lane location should be incremental.
2) Add morning/day/dusk/night detection in the beginning and automatically make parameter adjustments to account for the lighting conditions.

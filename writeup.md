# **Finding Lane Lines on the Road** 

## Writeup Report
---

> **Finding Lane Lines on the Road**

The goal of this project is to make a pipeline that finds on the road. The project is done using Python with OpenCv library and can be replicated in a Jupyter Notebook.

### The technique used is:
1. Color Conversion
2. Canny Edge Detection
3. Region of Interest Selection
4. Hough tranformation for Lane Detection 

[//]: # (Image References)


[image1]: ./Writeup_images/filtered.png "Filtered Image"
[image2]: ./Writeup_images/canny.png "Canny-Edge"
[image3]: ./Writeup_images/hough.png "Hough Transform"
[image4]: ./Writeup_images/super.png "Final Image"
[image5]: ./Writeup_images/average.png "Extrapolated Image"
---

> ## Reflection

### 1. The Pipeline for the first part of the Project is breifly explained below:
 * Loading the test images (RGB color-space)
 
 * The first step was to convert the RGB format image to HSL format and then applying a filter to extract white and yellow lane colors. (Tried working with RGB HSV format but didn't get good results) 

 ![image1]

 * Converted the HSL/filtered image to a grayscale image.

 * Applied Gaussian Blur to remove unwanted noise form the image.

 * Next step was to apply the Canny Edge Function in order to extract the edges from the image.

 ![image2]

 * Now, assuming that the camera is rigidly mounted on the car, I defined a region of interest. The Region of interest applies a mask over an image, which removes all the unecessary edges from the image.

 * Next step in the pipeline was to apply Hough Transform function in order to detect straight lines from the input image.

 ![image3]

 * The last step was to superimpose the Detected Lane Lines over the original image. This was accomplished using the weighted image function.

 ![image4] 

### 2. Second Part of the Project (Averaging Lines):
 After Successfully identifying lane lines using Hough transformation, our objective shifts on improving the lane lines. Basically we want only two lines representing the left and right lanes of the road.

> #### Improving the draw_lines() function:
 * The idea is to take points of the lines obtained by the Hough Transform function and calculate the average slopes and average intercepts for left as well as the right lane. Then using these two quantities we can easily replace the old lines with two average lines.

 * To do this, I created an empty lists to hold values for the slope & intercept/bias. 

 * Then filtered out the unwanted lines like vertical & horizontal lines.
 * Calculated the Average slope and intercept/bias for right as well as the left lane.
 * Then taking two y-coordinate values from the Region of Interest , calculated the corresponding x-coordinate values.
 * Using the two pairs of x,y values constructed the two average lines representing the left and right lane.

 ![image5]








 



>### 2. Identify potential shortcomings with your current pipeline


There are a few shortcomings to the current pipeline, the movement of lines through different frames is not smooth. Also the current pipeline is unable to keep up with curved road lanes and if any object/car enters our region of interest it could possibly be identified as a lane. The current pipeline also assumes that the color of lane lines as well as the environment remains the same.


> ### 3. Suggest possible improvements to your pipeline

A possible improvement would be to identify lane lines using a higher degree polynomial instead of lines. Some machine learning models would give us the same or better results with relatively less work.

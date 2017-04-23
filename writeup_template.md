#**Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1.My pipeline consisted of the following steps:

First, I converted the images to grayscale and applied gaussian smooting to the greyscale image to reduce noise in the image. I then applied the Canny algorithm to this image to detect edges with some trial and error to find appropriate values of the low and high thresholds. I then applied a mask to the detected to filter out edges that do not logically correspond to lane lines and keep the edges that may belong to the lane lines. The Hough Transform was then applied to remaining edges to identify lines. The parameters used for the Hough Transform were again found through trial and error after processing all of the provided images. After the Hough Transform, the lines were drawn on the original image and displayed to the user.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function. A description of my approach is provided:
    For each line, calculate the slope and intercept and separate the lines 
    into left and right by the sign of their slope (negative slope = left side)
    Additionally filter out lines with 'crazy' slopes; I made some assumptions and
    belive that the absolute value of the slope of a line we're interested in is 
    in between 0.4 and 1.0. 
    
    For the lines that correspond to the left hand side and have an acceptable slope value:
    1.)calculate the median slope and intercept values
    2.)Find the x-intercept of a line with median slope and intercept values 
            that goes through the bottom of the image
    3.)Sort the y points in decreasing order and select the point that is at 95% 
            of the length of the list of y points; 95% is to avoid an potential outliers
    4.)Calculate the x value for a line with the median slope and intercept value that crosses
       through the point calculated in step 3.
    5.)Draw a line through (x pt calculated in step 2, image y dimension) and
                            (x pt calculated in step 4, y pt calculated in step 3)
If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

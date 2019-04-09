# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline was fairly straightforward. 

1) First, I converted the images to grayscale.

2) Gaussian smoothing

3) Canny Transformation

4) Region Mask

5) Hough Transformation

6) Combine the weighted image/frame

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first figuring out how to implement the slope value to figure out which lines are the left and right. If you notice, any line coming from the right lane has to have a negative slope and any line coming from the left has to have a positive slope. So after figuring out how this divider works, I went forward and sorted the detected hough lines into left or right lane lines via the slope. After gathering the points I knew we're on which line, I used the np.polyfit function to gather the coefficients of the lines. From here, I tried playing with np.average but, in the end np.poly1d worked better for me and I was able to evaluate the best line of fit and connect a line between the two. 

If you'd like to include images to show how the pipeline works, here is how to include an image: 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the shadows interact with the environment. Such as with the challenege video which I was unable to complete, additionally this only works well on white and yellow images and only a certain subdivision of those. 

Another shortcoming is the harboring of outlier lines or when a line is incorrectly calculated, then it shouldnt be shown. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to implement a discriminator function that if it detects a line that is completely wrong, it could re-iterate the last line and continue on the next iteration after it, as far as the lines it shows. 

Another potential improvement could be to making the code more efficient. Althought this was my first time using jupyter notebook, it still takes some getting used to.
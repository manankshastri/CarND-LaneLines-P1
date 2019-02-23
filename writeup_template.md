# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

I divided the project into 2 parts - Part I: detecting line segments using the helper functions, Part II: connecting/extrapolating the 
line segments.

For both the parts, I converted the image into grayscale, did gaussian blur to the grayscaled image, extracted edges using canny, constructed a region of interest and used hough transform for detecting the line segments.

For Part I: 
1. After doing all the necessary steps, various parameters were tweaked for the desired output.
2. The outputs were saved.
3. I even tried the algorithm on the videos. It worked (the challenge video was an exception - not all the lanes were being detected).

For Part II:
1. I struggled initially, but I followed the comments in the draw_lines() function.
2. Firstly, I identified the lanes - whether the lane is a left lane or right lane by calculating the slope and assigning different colors when drawing lines. 
3. After identifying, I combined the coordinates of the line segments of both the lanes. Combining coordinates of the left lane to an empty list 1 and that of the right lane to list 2.
4. So, I had two arrays with coordinates of the line segments - list 1 with coordinates of line segments of the left lane and list 2 with coordinates of line segments of the right lane.
5. I averaged the points of list 1 and list 2, using numpy polyfit. Used the output of numpy polyfit to calculate x1 and x2 with y1 and y2 fixed and then constructed the lines using cv2 line. 
6. I also tried using another alternative to numpy polyfit - numpy linalg least square (least square fit). An error popped. 
7. The algorithm was implemented on the images. Parameters had to be modified to get the desired output. 
8. All the outputs were saved. 
9. Tried the same algorithm on the videos. It worked, but there is still room for improvement. 
10. For the challenge video, the algorithm didn't work - the lanes were not being detected properly. 


### 2. Identify potential shortcomings with your current pipeline


Shortcomings:
1. For Part 1, the combinations of the parameters yielded desired output on some of the images. I tried changing a few of the parameters in order to have consistent output, but it messed up. So, I chose those parameters where the lanes were detected in most of the images. 
2. For Part 2, the algorithm worked for all the images, with the desired output. But for video, the averaged line segments would not remain stable, shaking most of the time in the video.
3. For the challenge video, the averaged line segments were way out the desired path - even after modifying the parameters. 


### 3. Suggest possible improvements to your pipeline

There would be another way for averaging the line segments, probably more robust. 
For detecting the lanes in the video, there is still room for improvement.
I think modifying the parameters would help achieve the desired goal.


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

My pipeline consisted of 5 steps. 

  	img = grayscale(img_init)
    img = gaussian_blur(img,kernel_size)
    img = canny(img,low_threshold,high_threshold)
    img = region_of_interest(img, vertices)
    img = hough_lines(img, rho, theta, threshold, min_line_len, max_line_gap)
    img = weighted_img(img,img_init)

Since all functions except draw_lines() were finished, I will focus on what I changed
in draw_lines():

I adapt draw_lines() such that the angles of the hough lines (inputs) are calculated in order to seperate right and left lane line segements. 

Then, for each side respectively, left and right, a first-order polynomial is fitted onto the points of the hough lines (lane segments). 

Finally, the polynomials are drawn on the image img.

NOTE: I introduce two new functions:
1.fit_line(): 
To define the order of the polynomial, which shall be fitted onto the points of the hough lines. 
2.fit_line_points(): 
To define points of the fitted polynomial as input for cv2.polylines()


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

Currently, only a first-order polynomial is fitted. In the second step, a second-order
polynomial should be used. However, I encountered stabilization/fitting issues in the lower part of the picture, when there are no lane marking available (dotted lanes).

### 3. Suggest possible improvements to your pipeline

As described above, a second-order polynomial should used to have a better fit for the detected lanes. Especially, in curved roads, the first-order polynomial will not be sufficient anymore.




#**Finding Lane Lines on the Road** 

---

**The goals / steps of this project are the following:**
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Pipeline Description : 
	My pipeline consisted of 5 steps. 
	1. Loaded the video/image and converted it into grayscale.
	2. The grayscale image was darkened to improve contrast and improve recognition of bright lane lines.
	3. Gaussian smoothing (kernel size = 5) is applied to the image 
	4. Canny edge detection is applied (low threshold = 50 and high threshold = 150)
	5. Apply an image mask to remove 
	6. Apply Hough Tranform line detection algorithm 
	7. Draw the line segments denoting the detected right and left lane. This bit was tricky as it required the line segments within a lane to be joined and extrapolated to have the desired result. 
			1. We first separate all the lines and categories them as right or left lane on basis of their slope. 
			2. We then find the furthest points on the respective lanes (Xmax, Ymax, Xmin, Ymin).  While we find the furthest point, we remove improbable lines (for example - left lane lines cannot have x value greater than half of image width and vice versa for right lane)
			3. We use the furthest point to draw the lane lines.
	


###2. Potential shortcomings with the current pipeline
	1. The dimension of mask is set such that it works fine for a straight & flat road but starts to fail when the road either has a curve or a crest as it mistakes the bright background as edges.
	2. In case of a brighter road and yellow lane, edge detection becomes difficult. 


###3. Possible improvements to the pipeline
	1. In order to improve edge detection; we can convert image to HSV and construct yellow and white mask. Combining these two mask with bitwise OR to the darkened image could improve the edge detection on brighter roads. 
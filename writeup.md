# **Finding Lane Lines on the Road** 


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

**Required Files**

The submitted files of this project includes:
* The project code in a Jupyter notebook
* The output of test images and videos with original draw_lines() function
* The output of test images and videos with modified draw_lines() function
* The writeup file which described my pipeline

[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve_gray.jpg 				"Grayscale"
[image2]: ./test_images_output/solidWhiteCurve_edges.jpg 				"Edges"
[image3]: ./test_images_output/solidWhiteCurve_masked_edges.jpg 		"MaskedEdges"
[image4]: ./test_images_output/solidWhiteCurve_Hough_line_raw.jpg 		"HoughLineRaw"
[image5]: ./test_images_output/solidWhiteCurve_Hough_line_modified.jpg 	"HoughLineModified"
[image6]: ./test_images_output/solidWhiteCurve_output.jpg 				"Output"
---

### Reflection

### 1. Pipeline description

My pipeline consisted of 5 steps. 

**Step 1:** The image was converted to grayscale, here is an example of one test image:

![alt text][image1]

**Step 2:** The edges in the grayscale image were extracted by Canny edge detection methods:

![alt text][image2]

**Step 3:** The edge image was masked by a triangle region of interest:

![alt text][image3]

**Step 4:** The lines in masked edge image were detected by Hough transform. Since the lane lines can be segemented, I modified the draw_lines() function to draw a single line on the left and right lanes, respectively.

The original output of Hough lines detection:

![alt text][image4]

The modified output of Hough lines detection:

![alt text][image5]

To achieve the output above, I followed the instructions described in the code in Jupyter Notebook. First I calculated the slopes of all lines detected in the masked edge image. Then I selected a reference slope for left and right lane line, respectively. Also I defined a boundary to allow some variations and make the pipeline more robust. Finally all the accepted slopes and points for left and right lane lines are averaged, which were used to extrapolate to the top and bottom of the lane.

**Step 5:** The generated lane lines were added to the original image:

![alt text][image6]


### 2. Potential shortcomings with current pipeline

One potential shortcoming would be the shaking of detected lines comparing with the example result. It seems that the selected averaged points for each lane lines were not that continuous and smooth.

Another shortcoming could be the robustness of the pipeline. The results are highly affected by the selection of the parameters, especially the Canny edge detection and Hough line detection. For example, in the challenge scenario, due to the sunlight variation, it is difficult to decide the boundary in Canny edge detection function.


### 3. Possible improvements to current pipeline

For the shaking of detected lane lines, a possible improvement would be to calculate the mean slope of lane lines with respect to the length of line segements. The longer the line segments are, the higher the slope weights are. Also, a low-pass filter could be applied to the average points of the lane lines to smooth the results especially for an image sequence.

For the missing edge detection in the challenge scenario, a potential improvement could be to adjust the brightness of the image in the region of interest. 

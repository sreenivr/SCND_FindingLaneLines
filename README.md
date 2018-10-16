# **Finding Lane Lines on the Road** 

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

The goal of this project is to implement a pipeline that finds lane lines on the road. I have used Python and OpenCV to implement the pipeline. I started with implementation of lane finding pipeline on an image. Then the same pipeline was applied on a videos. Videos are essentially series of images.

Following are the steps in my pipeline.

1. Convert the image to gray scale
2. Noise removal using GaussianBlur. 
3. Canny edge detection
4. Region of interest selection
5. Hough transform for line segment detection
6. Computing left and right lanes by extrapolating the line segment.

Converting the image to gray scale makes it easier to implement algorithms like edge detection. I used OpenCV function cv2.cvtColor(img, cv2.COLOR_RGB2GRAY) to accomplish this step.

Edges are detected when there is high rate of change of intensity value in a image function. Noise removal helps to remove any unwanted edges detected in the next step. I used the OpenCV function cv2.GaussianBlur() to perform this step.

The next step was to use the OpenCV function cv2.Canny() to perform Canny Edge detection.

There are can be many edges and lines in the given image. One of the main challenges was to find the region of interest in the image such that unwanted lines are removed. This is one of the disadvatages of the current algorithm that I have implemented. This implementation expects the region interest in a specific region in the given image. The region of interest is computed as a function of width and height of the given image. This implementation will fail if the actual lane lines are outside the region of interest.

Hough transform is used to detect the line segments in the given image. Lane lines can be a solid line or a doted line. In case of doted line, this implementation extrapolates or avarages the slope/offset of the line segments. Hough transform returns a set of lines. Based on its slope, we can detect whether it belongs to left or right lane. 

Here are few example images after the lane lines are marked.

<img src="test_image_output/solidWhiteCurve.jpg" width="480" alt="Combined Image" />
<img src="test_image_output/solidYellowCurve2.jpg" width="480" alt="Combined Image" />

Finally, the pipeline was applied on a real video file and see the output below.

<img src="test_videos_output/solidWhiteRight.mp4" width="480" alt="Combined Image" />

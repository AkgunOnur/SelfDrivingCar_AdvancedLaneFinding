# Advanced Lane Finding

In this project, the goal is to identify the lane boundaries in a video stream

**Advanced Lane Finding Project**
---
The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./examples/camera_calibration.JPG "Camera Calibration"
[image2]: ./examples/undistortion.JPG "Image Undistortion"
[image3]: ./examples/undistortion2.JPG "Image Undistortion"
[image4]: ./examples/threshold.JPG "Thresholded image"
[image5]: ./examples/threshold2.png "Thresholded image"
[image6]: ./examples/threshold3.png "Thresholded image"
[image7]: ./examples/hist.png "Frequency of the steering angles"
[image8]: ./examples/left_augment.png "Distorted left image"
[image9]: ./examples/right_augment.png "Distorted right image"

## Camera Calibration 

The OpenCV functions `findChessboardCorners` and `calibrateCamera` are used for camera calibration. A number of images of a chessboard, taken from different angles with the same camera. Arrays of object points, corresponding to the location of internal corners of a chessboard, and image points, the pixel locations of the internal chessboard corners determined by `findChessboardCorners`, are fed to `calibrateCamera` which returns camera calibration and distortion coefficients. These can then be used by the OpenCV `undistort` function to undo the effects of distortion on any image produced by the same camera. Generally, these coefficients will not change for a given camera (and lens). The image below depicts the process

![alt text][image1]

The images below show the results of `undistort` function, using the calibration and distortion coefficients, to one of the chessboard images

![alt text][image2]
![alt text][image3]

To get thresholded binary image, a few filters which are Sobel on x and y axes, direction filter, s channel filter for a HLS image are applied to the image. The image below shows the result

![alt text][image4]
![alt text][image5]

To detect lane lines in a more robust way,  L channel of the HLS color space is used to isolate white lines and the B channel of the LAB colorspace is used to isolate yellow lines. As it can be seen below, this approach gives better results than before.  I did not use any gradient thresholds in my pipeline. Each filter's threshold values are adjusted so that the result has least tolerant to the light. 

![alt text][image5]

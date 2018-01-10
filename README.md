# Advanced Lane Finding

In this project, the goal is to identify the lane boundaries in a video stream

** Advanced Lane Finding Project **
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
[image4]: ./examples/center_augment.png "Distortion applied on the image"
[image5]: ./examples/left.png "Image from left camera"
[image6]: ./examples/right.png "Image from right camera"
[image7]: ./examples/hist.png "Frequency of the steering angles"
[image8]: ./examples/left_augment.png "Distorted left image"
[image9]: ./examples/right_augment.png "Distorted right image"

## Camera Calibration 

The OpenCV functions `findChessboardCorners` and `calibrateCamera` are used for camera calibration. A number of images of a chessboard, taken from different angles with the same camera. Arrays of object points, corresponding to the location of internal corners of a chessboard, and image points, the pixel locations of the internal chessboard corners determined by `findChessboardCorners`, are fed to `calibrateCamera` which returns camera calibration and distortion coefficients. These can then be used by the OpenCV `undistort` function to undo the effects of distortion on any image produced by the same camera. Generally, these coefficients will not change for a given camera (and lens). The image below depicts the process

![alt text][image1]

The images below show the results of `undistort` function, using the calibration and distortion coefficients, to one of the chessboard images:

![alt text][image2]
![alt text][image3]


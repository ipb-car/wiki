<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Calibration](#calibration)
  - [Intrinsic Camera calibration](#intrinsic-camera-calibration)
  - [Sensor to Sensor calibration](#sensor-to-sensor-calibration)
    - [Camera to Camera](#camera-to-camera)
    - [Camera to LiDAR](#camera-to-lidar)
    - [LiDAR to LiDAR](#lidar-to-lidar)
    - [SBG to GPS](#sbg-to-gps)
    - [LiDAR to SBG](#lidar-to-sbg)
    - [How to get the other transformations?](#how-to-get-the-other-transformations)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Calibration

In this page we will provide some insights in how the geometric calibration between the sensors is done. This means finding the transformation between the different sensory coordinate systems.
These are the sensors we need to calibrate w.r.t each other:

1. 4 Basler Cameras (Front, Rear, Left, Right)
2. 1 Horizontal and 1 vertical Ouster LiDAR
3. SBG IMU + Dual Antenna GPS

## Intrinsic Camera calibration

The cameras are the only sensors where we also compute the intrinsic calibration (Camera constant, principal point, shear, scale + nonlinearities). For this, we use [TCC](https://gitlab.ipb.uni-bonn.de/ipb-team/ipb-tools/tcc). The calibration is usually done by Thomas.

## Sensor to Sensor calibration

The calibration between the sensors is basically always done using a global reference. The transformation is not estimated directly between the sensors but rather sensor 1 to reference and sensor 2 to reference. The transformation between the sensors can then be obtained by the inverse of one transformation times the other transformation.

### Camera to Camera

For the camera to camera to camera calibration the intrinsics need to be estimated in the first place. The calibration is done using a bundle adjustment (part from the BACS project) with apriltags. For this, we have a calibration room with apriltags. The apriltag positions are estimated using the point cloud of a FARO TLS. The point cloud is projected to the walls/ceiling and can then be found using classic opencv to find the apriltag coordinates. For the calibration, mutliple corresponding images are recorded in stop-and-go. These serve as input for the BACS which outputs us with the camera poses (in the TLS coordinate system) of each camera at each timestamp as well as the relative transformation between the camereas.

### Camera to LiDAR

To estimate the transformation between the camera frame and the LiDAR frame we need to find the poses of the LiDAR scanners in the frame of the TLS at the same timestamps as the camera images from camera-to-camera calibration. So we not only store the images but also the point clouds from the LiDAR. The poses of the LiDARs in the TLS frame are simply computed using ICP between the LiDAR point clouds and the TLS. We use the poses from the cameras + an initial estimate of the calibration as initial guess for the ICP.
The relative transformation between the poses from the cameras and the LiDAR is the camera to LiDAR calibration.

### LiDAR to LiDAR

The LiDAR to LiDAR calibration can already be done with the data we have computed before. We simply take the relative transformation between the two LiDAR poses at the same timestamps (as previous with LiDAR and camera poses).

### SBG to GPS

The SBG IMU needs the relative transformation to the GPS antennas. This is simply done using a measuring tape. These values are refined in the EKF.

### LiDAR to SBG

For the reference, we use a point cloud in GPS coordinates which has been recorded by the IGG department using a TLS and some GPS receivers. Similar procedure as before: first estimate poses using ICP between the LiDAR scanner and the TLS. Second, compute the relative transformation between the poses of the LiDAR scanner and the SBG.

### How to get the other transformations?

If we now want the transformation between the other sensors, we need to chain the corresponding calibration matrices.
Small example, e.g. from camera left to SBG: camera left to camera front, camera front to LiDAR horizontal, LiDAR horizontal to SBG.

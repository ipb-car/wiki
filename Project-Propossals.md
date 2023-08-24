<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [9-axis IMU](#9-axis-imu)
- [Altimeter](#altimeter)
- [LiDAR-LiDAR calibration](#lidar-lidar-calibration)
- [New GPS](#new-gps)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

This is the starting point to seed new ideas for the ipb-car mount. If an idea is listed here means that is not yet part of our issue tracking system and has no assignee. Thus it's ready to be taken by anyone :)

## 9-axis IMU

We are currently working on an IMU-LiDAR-GPS pipeline to obtain GT poses of the vehicle while we drive through the city. We started using LIO-SAM as a baseline and for that, we need a 9-axis IMU. The one we have on each Ouster LiDAR is 6-axis and therefore won't work out of the box.

We need to buy a new IMU, evaluate, put it on the car mount, calibrate, etc.

## Altimeter

Cyrill and Nacho are completely bored about LiDAR odometry pipelines drifting on the Z-axis. It's a very well-known issue but it's mostly hidden in papers due to the fact that everyone uses 2D plots and doesn't show this problem. Adding a simple altimeter sensor to the car, we should be able to lock the z-coordinate estaimte. At least giving some min-max bounds. This could be also integrated into a pose-graph scheme using the altimeter sensor output as part of the sensor data.

## LiDAR-LiDAR calibration

We have 2 lidars, but we don't have the calibration between them. This doesn't seem like the most complex task ever but I guess is also not trivial to solve. As starting point just measuring with a tape the transformation between both LiDARS might be enough. But we should put the sensors in the calibration room and aim for more precise calibration.

## New GPS

We are not yet convinced with the Emlid-GPS we have right now. Lasse from the IGG department has a nice setup with 2 GPS. We already asked him to help us with this matter. The idea would be to record data with our GPS and theirs and compare it to see if one is more accurate than the other one. If the double-GPS looks more precise, then we should definitely switch to that configuration.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Precise Time Protocol](#precise-time-protocol)
  - [Configuration](#configuration)
  - [What people says](#what-people-says)
    - [nuScenes](#nuscenes)
    - [KITTI](#kitti)
    - [Ford Campus](#ford-campus)
  - [PTP Online Documentation](#ptp-online-documentation)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Precise Time Protocol

The Precision Time Protocol (PTP) is a protocol used to synchronize clocks throughout a computer network. On a local area network, it achieves clock accuracy in the sub-microsecond range, making it suitable for measurement and control systems (Wikipedia: [Precision Time Protocol](https://en.wikipedia.org/wiki/Precision_Time_Protocol)).

## Configuration

In order to utilize the PTP protocol for the Raspberry Pi, configure it by
following the below steps:

1. [Gps Clock Synchronization](Precise-Time-Protocol%3AGps-Clock-Synchronization)
2. [Enable ptp for rpi](Precise-Time-Protocol%3AEnable-ptp-for-rpi)
3. [PTP configuration](Precise-Time-Protocol%3APTP-configuration)
4. [PTP monitoring](Precise-Time-Protocol%3APTP-monitoring)
5. [PTP references](Precise-Time-Protocol%3APTP-references)

## What people says

You can find below how other people solve the time synchronization
between multiple sensors. If you find some other example, please provide a link
to the white paper where the technique is being described and a link to the
datasets page.

### [nuScenes](https://www.nuscenes.org/)

> In order to achieve good cross-modality data alignment between the lidar and
> the cameras, the exposure of a camera is triggered when the top lidar sweeps
> across the center of the camera’s FOV. The timestamp of the image is the
> exposure trigger time; and the timestamp of the lidar scan is the time when
> the full rotation of the current lidar frame is achieved. Given that the
> camera’s exposure time is nearly instantaneous, this method generally yields
> good data alignment.
>
> The cameras run at 12Hz while the lidar runs at 20Hz. The 12 camera exposures
> are spread as evenly as possible across the 20 lidar scans, so not all lidar
> scans have a corresponding camera frame.
>
> --<cite>[paper][1]</cite>

### [KITTI](http://www.cvlibs.net/datasets/kitti/raw_data.php)

> In order to synchronize the sensors, we use the timestamps of the Velodyne 3D
> laser scanner as a reference and consider each spin as a frame. We mounted a
> reed contact at the bottom of the continuously rotating scanner, triggering
> the cameras when facing forward. This minimizes the differences in the range
> and image observations caused by dynamic objects. Unfortunately, the GPS/IMU
> system cannot be synchronized that way. Instead, as it provides updates at 100
> Hz, we collect the information with the closest timestamp to the laser scanner
> timestamp for a particular frame, resulting in a worst-case time difference of
> 5 ms between a GPS/IMU and a camera/Velodyne data package. Note that all
> timestamps are provided such that positioning information at any time can be
> easily obtained via interpolation. All timestamps have been recorded on our
> host computer using the system clock.
>
> --<cite>[paper][2]</cite>

### [Ford Campus](http://robots.engin.umich.edu/SoftwareData/Ford)

> In order to minimize the latency in data capture, all of the sensor load is
> evenly distributed across the four quadcore processors installed at the back
> of the truck. Time synchronization across the computer cluster is achieved by
> using a simple network time protocol (NTP) [Mills, 2006] like method whereby
> one computer is designated as a “master”and every other computer continually
> estimates and slews its clock relative to master’s clock. This is done by
> periodically exchanging a small packet with the master and measuring the time
> it takes to complete the round trip. We estimate the clock skew to be upper
> bounded by 100 µs based upon observed round-trip packet times.
>
> When sensor data is received by any of these synchronized host computers, it
> is timestamped along with the timestamp associated with the native hardware
> clock of the sensor device. These two timestamps are then merged according to
> the algorithm documented in [Olson, 2010] to determine a more accurate
> timestamp estimate. This sensor data is then packaged into a Lightweight
> Communication and Marshalling (LCM) [Huang et al., 2010] packet and is
> transmitted over the network using multicast user datagram protocol (UDP).
> This transmitted data is captured by a logging process, which listens for such
> packets from all the sensor drivers, and stores them on the disk in a single
> log file. The data recorded in this log file is timestamped again, which
> allows for synchronous playback of the data later on.
>
> --<cite>[paper][3]</cite>

[1]: https://arxiv.org/pdf/1903.11027.pdf
[2]: http://www.cvlibs.net/publications/Geiger2013IJRR.pdf
[3]: http://robots.engin.umich.edu/publications/gpandey-2010b.pdf

## PTP Online Documentation

This are **some** of the sources we've used to develop the PTP network for the
ipb_car:

- [Configuring PTP Using ptp4l :: Fedora Docs Site][4]
- [Gps ptp timesync report by Ajin Tom - issuu][5]
- [Implementation and Performance Analysis of Precision Time Protocol on Linux based System-On-Chip Platform][6]
- [LinuxPPS: LinuxPPS wiki][7]
- [LinuxPPS: Technical Information][8]
- [Building a Raspberry-Pi Stratum-1 NTP Server][9]
- [Quick-start Raspberry Pi NTP server][10]
- [Precision Time Protocol on Linux ~ Introduction to linuxptp][11]
- [twteamware/raspberrypi-ptp][12]
- [Kernel building - Raspberry Pi Documentation][13]
- [timesync: ptp master · Wiki · ipb-team / robots / ipb-car / ipb-car-docs · GitLab][14]
- [Allied Vision IEEE 1588 PTP Camera Manuals(Philipp's Cameras)][15]

[4]: https://docs.fedoraproject.org/en-US/fedora/rawhide/system-administrators-guide/servers/Configuring_PTP_Using_ptp4l/
[5]: https://issuu.com/ajintom/docs/gps_ptp_timesync_report
[6]: http://www.creative-technologies.de/wp-content/uploads/2018/05/Master_Project__PTP_1588.pdf
[7]: http://linuxpps.org/doku.php/start
[8]: http://linuxpps.org/doku.php/technical_information
[9]: https://www.satsignal.eu/ntp/Raspberry-Pi-NTP.html#pps-check
[10]: https://www.satsignal.eu/ntp/Raspberry-Pi-quickstart.html
[11]: https://events.static.linuxfound.org/sites/events/files/slides/lcjp14_ichikawa_0.pdf
[12]: https://github.com/twteamware/raspberrypi-ptp/blob/master/patches/0001-smsc95xx-use-generic-ethtool_op_get_ts_info-callback.patch
[13]: https://www.raspberrypi.org/documentation/linux/kernel/building.md
[14]: https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docs/wikis/timesync%3A-ptp-master
[15]: https://cdn.alliedvision.com/fileadmin/content/documents/products/cameras/various/appnote/GigE/PTP_IEEE1588_with_Prosilica_GT_GC_Manta.pdf

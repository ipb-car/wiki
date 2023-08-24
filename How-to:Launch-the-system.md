<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Before launching](#before-launching)
- [Installation](#installation)
- [Build](#build)
- [Launch](#launch)
- [Record](#record)
- [[IMPORTANT!] Extract data and code](#important-extract-data-and-code)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Follow this procedure if you want to launch the system successfully:

## Before launching

Before launching the system be sure of respecting these two steps:

- (If you are testing indoors) place the GPS antenna outside such that it can receive GPS signal.
- Visually inspect connections and the general setup.
- Turn on power of the battery (turn the key). Also, turn on the power of and connect to the hub.
- Connect to polenta (host).
- If you forgot the password, ask rongo ;P
- Set the network on polenta to that of the thunderbolt one.
- Check all code on the system is the latest.

## Installation

You only need to clone to code into a local ROS workspace in the host machine:

```sh
mkdir -p ~/ipb_car/ros_ws/ && cd ~/ipb_car/ros_ws/
git clone --recurse-submodules git@gitlab.ipb.uni-bonn.de:ipb-team/robots/ipb-car/meta-workspace src/
```

## Build

```sh
cd ~/ipb_car/ros_ws/src/
make build
```

## Launch

```sh
cd ~/ipb_car/ros_ws/src/
make launch
```

## Record

```sh
cd ~/ipb_car/ros_ws/src/
make record
```

## [IMPORTANT!] Extract data and code

A random drunkard reserves the right to wipe all bags and code! Remember to push or copy out your bag files!

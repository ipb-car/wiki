<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [GPS Emlid Reach Troubleshooting](#gps-emlid-reach-troubleshooting)
  - [Ethernet connection](#ethernet-connection)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# GPS Emlid Reach Troubleshooting

## Ethernet connection

![diagram](https://community.emlid.com/uploads/default/original/3X/8/3/83083cfb70a7d862ac46418cb00366eeede6647b.jpeg)

So far we haven't been able to connect the GPS through an Ethernet connection.
The idea behind this is to connect the GPS to the switch we have in the car
mount and access all the sensors via the Network interface.

We have dived deep into this problem and we found that it's related to some
missing drivers for the Linux kernel in the local GPS computer. We've written an
email and a community post to Emlid people and all the details can be found
there:

[Connecting Reach RS2 to Laptop using a Ethernet RJ45 Connector](https://community.emlid.com/t/connecting-reach-rs2-to-laptop-using-a-ethernet-rj45-connector/16051)

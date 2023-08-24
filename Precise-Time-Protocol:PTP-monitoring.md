<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [PTP Network Monitoring](#ptp-network-monitoring)
  - [Check ptp4l](#check-ptp4l)
    - [CURRENT_DATA_SET](#current_data_set)
    - [PARENT_DATA_SET](#parent_data_set)
    - [DEFAULT_DATA_SET](#default_data_set)
  - [Query ptp4l](#query-ptp4l)
  - [Restart ptp4l](#restart-ptp4l)
  - [Additional information](#additional-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# PTP Network Monitoring

In this page you will find a series of commands that will help you to check the `linuxptp` daemon called `ptp4l`.

But first download the linux ptp tools:

```bash
$ sudo apt install ethtool linuxptp pps-tools lshw
```

## Check ptp4l

The PTP management client, **pmc**, can be used to obtain additional information from other devices connected to the PTP inside the network.

#### CURRENT_DATA_SET

_Useful for retrieving the offset from the master._

```bash
$ sudo pmc -u 'GET CURRENT_DATA_SET'
```

```bash
sending: GET CURRENT_DATA_SET
	bc0fa7.fffe.00090c-1 seq 0 RESPONSE MANAGEMENT CURRENT_DATA_SET
		stepsRemoved     1
		offsetFromMaster 215411.0
		meanPathDelay    41328.0
	dca632.fffe.2ccd2c-1 seq 0 RESPONSE MANAGEMENT CURRENT_DATA_SET
		stepsRemoved     0
		offsetFromMaster 0.0
		meanPathDelay    0.0
```

- `stepsRemoved` is the number of communication paths to the grandmaster clock.
- `offsetFromMaster` and master_offset is the last measured offset of the clock from the master in nanoseconds.
- `meanPathDelay` is the estimated delay of the synchronization messages sent from the master in nanoseconds.

#### PARENT_DATA_SET

Get information from every sync device of their parent (master) device.

```bash
$ sudo pmc -u 'GET PARENT_DATA_SET'
```

```bash
sending: GET PARENT_DATA_SET
	bc0fa7.fffe.00090c-1 seq 0 RESPONSE MANAGEMENT PARENT_DATA_SET
			parentPortIdentity                    dca632.fffe.2ccd2c-1
			parentStats                           0
			observedParentOffsetScaledLogVariance 0xffff
			observedParentClockPhaseChangeRate    0x7fffffff
			grandmasterPriority1                  0
			gm.ClockClass                         6
			gm.ClockAccuracy                      0x31
			gm.OffsetScaledLogVariance            0xffff
			grandmasterPriority2                  128
			grandmasterIdentity                   dca632.fffe.2ccd2c

	...
```

#### DEFAULT_DATA_SET

Get information realtive to the default data set of each sync device.

```bash
$ sudo pmc -u 'GET DEFAULT_DATA_SET'
```

```bash
sending: GET DEFAULT_DATA_SET
	bc0fa7.fffe.00090c-1 seq 0 RESPONSE MANAGEMENT DEFAULT_DATA_SET
		twoStepFlag             1
		slaveOnly               1
		numberPorts             1
		priority1               128
		clockClass              255
		clockAccuracy           0xfe
		offsetScaledLogVariance 0xffff
		priority2               128
		clockIdentity           bc0fa7.fffe.00090c
		domainNumber            0
	...
```

## Query ptp4l

`journalctl` can be used to query the `ptp4l` output. This is useful for understanding what is happening while the devices try to synchronize.

```bash
$ journalctl -f -u ptp4l
```

```bash
-- Logs begin at Mon 2019-10-07 17:17:01 CEST. --
Oct 07 18:09:49 ipbcar systemd[1]: Started Precision Time Protocol (PTP) service.
Oct 07 18:09:49 ipbcar ptp4l[931]: [583.895] port 1: INITIALIZING to LISTENING on INIT_COMPLETE
Oct 07 18:09:49 ipbcar ptp4l[931]: [583.896] port 0: INITIALIZING to LISTENING on INIT_COMPLETE
Oct 07 18:09:56 ipbcar ptp4l[931]: [590.964] port 1: LISTENING to MASTER on ANNOUNCE_RECEIPT_TIMEOUT_EXPIRES
Oct 07 18:09:56 ipbcar ptp4l[931]: [590.964] selected local clock dca632.fffe.2ccd2c as best master
Oct 07 18:09:56 ipbcar ptp4l[931]: [590.964] assuming the grand master role

```

## Restart ptp4l

If you are having problem with the protocol, then you may want to restart the service.

```bash
$ sudo systemctl restart ptp4l
```

## Additional information

Check out this Github repository where you can find really detailed information and useful commands for the `linuxptp` daemon:

- https://github.com/Mellanox/mlxsw/wiki/Precision-Time-Protocol

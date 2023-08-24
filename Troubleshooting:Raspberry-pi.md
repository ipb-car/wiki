<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Connect through ethernet using DHCP](#connect-through-ethernet-using-dhcp)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Let's pretend that the pi is not working for some reason, then you will need to connect to it.

If you never managed to finish the [setup](https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docs/-/wikis/Setup:Rpi-setup) then you could prey that it has [**DHCP enabled**](ipb-team/robots/ipb-car/raspberry/pi-gen#2). If the pi doesn't have DHCP enabled then you should connect through its [Wifi hotspot](https://gitlab.ipb.uni-bonn.de/ipb-team/robots/ipb-car/docs/-/wikis/Setup:Rpi-setup#wifi-hotspot)

## Connect through ethernet using DHCP

Run this command on your local desktop machine(or your dev machine)

The DHCP range in our ipb network is `131.220.233.150-195`, thus:

```bash
nmap -sV -p 22 131.220.233.150-195
```

Basically, this will scan all the devices connected to the ipb-net and waiting
for a DHCP address, this reduces the search space a lot, and thus the time you
spend figuring out which IP address the RPI4 got.

The output should look similar to this one:

```bash
$ nmap -sV -p 22 131.220.233.150-195

Starting Nmap 7.60 ( https://nmap.org ) at 2019-10-07 17:00 CEST
Nmap scan report for 131.220.233.180
Host is up (0.00036s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for 131.220.233.185
Host is up (0.00054s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Raspbian 10 (protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

We really only care about our little friend, in this particular case `131.220.233.185`:

```bash
Nmap scan report for 131.220.233.185
Host is up (0.00054s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Raspbian 10 (protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Now it's time to ssh into the board!

```bash
ssh pi@131.220.233.185
```

- username: pi
- password: ipb-car

If you did everything correctly, then you should have a connection to Raspberry Pi through
ssh:

```bash
ivizzo (master) ssh pi@131.220.233.185
The authenticity of host '131.220.233.185 (131.220.233.185)' can't be established.
ECDSA key fingerprint is SHA256:prlnDb6GImDhlziTkod9yiTXKw9EMbE//W+xAEokneM.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '131.220.233.185' (ECDSA) to the list of known hosts.
pi@131.220.233.185's password:
Linux raspberrypi 4.19.75-v7l+ #1270 SMP Tue Sep 24 18:51:41 BST 2019 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.

pi@raspberrypi:~ $
```

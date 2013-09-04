Some info about how to install [Debian/GNU Linux](http://www.debian.org) on a DLink DNS-320L NAS (on the SATA drive).


Serial port
-----------

First of all you need a working serial console. The serial port is located next to the USB port (see the picture). You need to do some soldering and use a serial cable such as the Nokia CA-42 or DKU-5 data cable. The serial pinout is [4 3 2 _ 1], where 1 is RX (the red cable in the picture), 3 is GND (the orange cable), and 4 is TX (the yellow cable). Pin 1 is labeled "JP1".


Building the root file system
-----------------------------

The easiest approach to create the root file system is to use debootstrap and then QEMU. The approach is well documented at [http://www.digriz.org.uk/debian/debootstrap](http://www.digriz.org.uk/debian/debootstrap).

Once the root file system is ready, you could try it by copying it onto an USB stick. Make sure you preserve all file system attributes (e.g., use cp -a).

To test the new root file system you need to tell the kernel that the file system is on the USB stick:

    Marvell>> setenv ethaddr [any MAC address]
    Marvell>> setenv bootargs console=ttyS0,115200 root=/dev/sdc1 usb-storage.delay_use=0 rootdelay=1 rw
    Marvell>> boot

As MAC address you could use the real MAC address of the ethernet card. A random MAC address works as well. You might need to replace /dev/sdc1 with /dev/sdb1 if you only have on SATA disk attached.

If everything works properly you should see the login prompt and be able to login.

Installing the new root file system on the SATA disk
----------------------------------------------------

You need to create a small partition on the disk (e.g., 4GB), format it, and then copy the content of the USB stick in the partition. Again, make sure all the file attributes are preserved.


To test the new root file system you need to reboot tell the kernel that the file system is now on the SATA disk:

    Marvell>> setenv ethaddr [any MAC address]
    Marvell>> setenv bootargs console=ttyS0,115200 root=/dev/sda1 usb-storage.delay_use=0 rootdelay=1 rw
    Marvell>> boot

If everything works properly you should see the login prompt and be able to login. 

Booting from the SATA disk by default
-------------------------------------

Save in the nvram the new kernel command line:

    Marvell>> setenv ethaddr [your MAC address]
    Marvell>> setenv bootargs console=ttyS0,115200 root=/dev/sda1 usb-storage.delay_use=0 rootdelay=1 rw
    Marvell>> savenev


Temperature sensor & fan
------------------------

You can use the fan-daemon.py script to automatically control the speed of the fan depending on the temperature of the board. 

Tweaking the installation
-------------------------

Once the base system is running you can partition the rest of the space, configure the RAID, etc. Just make sure you have all the necessary devices.

If you want to spin-down the hard-drive, you might need to monitor disk accesses to figure out which processes are accessing the disk (echo 1 > /proc/sys/vm/block_dump). There are several tutorials on the web that explain how to use tmpfs to allow the disks to spindown.


Links
-----

- [http://jamie.lentin.co.uk/devices/dlink-dns325](http://jamie.lentin.co.uk/devices/dlink-dns325)
- [http://blog.aboehler.at/2013/09/arch-linux-on-the-dns-320l/](http://blog.aboehler.at/2013/09/arch-linux-on-the-dns-320l/)
- [ftp://ftp.dlink.pl/dns/dns-320L/driver_software/](ftp://ftp.dlink.pl/dns/dns-320L/driver_software/)


Thanks
------

- [Jamie Lentin](http://jamie.lentin.co.uk/)
- [Roberto Paleari](http://roberto.greyhats.it) (for the thermal table)

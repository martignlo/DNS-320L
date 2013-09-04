Some info about how to get full control of a DLink DNS-320L NAS. I installed
Debian/GNU Linux (on the SATA drive).


Serial port
-----------

The serial port is located next to the USB port (see the picture). You need to
do some soldering and use a serial cable such as the Nokia CA-42 or DKU-5 data
cable. The serial pinout is [4 3 2 _ 1], where 1 is RX (the red cable in the
picture), 3 is GND (the orange cable), and 4 is TX (the yellow cable). Pin 1 is
labeled "JP1".


Temperature sensor & fan
------------------------

You can use the fan-daemon.py script to automatically control the speed of the
fan depending on the temperature of the board. 


Links
-----

- [http://jamie.lentin.co.uk/devices/dlink-dns325](http://jamie.lentin.co.uk/devices/dlink-dns325)


Thanks
------

- [Roberto Paleari](http://roberto.greyhats.it) (for the thermal table)
- [Jamie Lentin](http://jamie.lentin.co.uk/)

MAX7219 Driver
==============

Interfacing LED matrix displays with the MAX7219 driver 
[[PDF datasheet](https://raw.github.com/rm-hull/max7219/master/doc/MAX7219-datasheet.pdf)] 
in Python using hardware SPI on the Raspberry Pi. The particular kit I bought 
can be acquired for a few pounds from 
http://www.banggood.com/MAX7219-Dot-Matrix-Module-DIY-Kit-SCM-Control-Module-For-Arduino-p-72178.html?currency=GBP 

This library has recently had a major overhaul, and is not compatible with the earlier version. 
It now supports:

* multiple cascaded devices
* LED matrix and seven-segement variants

![max7219 matrix](https://raw.github.com/rm-hull/max7219/master/doc/images/devices.jpg)

Pre-requisites
--------------
Ensure that the SPI kernel driver is enabled:

    $ dmesg | grep spi
    [    3.769841] bcm2708_spi bcm2708_spi.0: master is unqueued, this is deprecated
    [    3.793364] bcm2708_spi bcm2708_spi.0: SPI Controller at 0x20204000 (irq 80)

And that the devices are successfully installed in /dev:

    $ ls -l /dev/spi*
    crw------- 1 root root 153, 0 Jan  1  1970 /dev/spidev0.0
    crw------- 1 root root 153, 1 Jan  1  1970 /dev/spidev0.1
    
Follow the advice in the references below if the devices do not appear before
proceeding.

GPIO pin-outs
-------------
The breakout board has an two headers to allow daisy-chaining:

| Board Pin | Name | Remarks | RPi Pin | RPi Function |
|--------:|:-----|:--------|--------:|--------------|
| 1 | VCC | +5V Power | 2 | 5V0 |
| 2 | GND | Ground | 6 | GND |
| 3 | DIN | Data In | 19 | GPIO 10 (MOSI) |
| 4 | CS | Chip Select | 24 | GPIO 8 (SPI CS0) |
| 5 | CLK | Clock | 23 | GPIO 11 (SPI CLK) |

Building & Installing
---------------------
The [SPI-Py](https://github.com/lthiery/SPI-Py) C-extension has already been 
included in the source directory, so to build and install: 

For Raspian:

    $ sudo apt-get install python-dev
    $ sudo python setup.py install

For Arch Linux:

    # pacman -Sy base-devel python2
    # python2 setup.py install


Examples
--------
Run the example code as follows:

    $ sudo python examples/matrix_test.py

or

    $ sudo python examples/sevensegment_test.py

*NOTE:* By default, SPI is only accessible by root (hence using `sudo` above). Follow these 
instructions to create an spi group, and adding your user to that group, so you don't have to
run as root: http://quick2wire.com/non-root-access-to-spi-on-the-pi

References
----------
* http://hackaday.com/2013/01/06/hardware-spi-with-python-on-a-raspberry-pi/
* http://gammon.com.au/forum/?id=11516
* https://github.com/lthiery/SPI-Py
* http://louisthiery.com/spi-python-hardware-spi-for-raspi/
* http://www.brianhensley.net/2012/07/getting-spi-working-on-raspberry-pi.html
* http://raspi.tv/2013/8-x-8-led-array-driven-by-max7219-on-the-raspberry-pi-via-python
* http://quick2wire.com/non-root-access-to-spi-on-the-pi

License
-------
See [MIT License](https://github.com/rm-hull/max7219/blob/master/LICENSE.md).

Portions of this code are derived from https://github.com/lthiery/SPI-Py
which includes the following license notice:

> COPYRIGHT (C) 2012 Louis Thiery. All rights reserved. 
Further work by Connor Wolf.

> This program is free software; you can redistribute it and/or modify it
under the terms of the GNU General Public License V2 as published by the 
Free Software Foundation.

> LIABILITY
>This program is distributed for educational purposes only and is no way 
suitable for any particular application, especially commercial. There is
no implied suitability so use at your own risk!



# Basic requirements

Hardware
-------

In addition to the Magnolia, you're going to need a 5V happy LED. A lot of 3V+ LEDs can handle the 5V from an arduino, but lower voltage ones tend to shine bright and short when powered up. You're going to need a push button switch of some sort, and for later lessons there will be a need for other components.

* a whole bunch of LEDs
* light sensisitive resistor
* prototyping board (optional, but really useful) and jumper cables.
* 8-bit shift register
* piezo or other low resistance speaker

Software
-----

You're going to need to download the arduino IDE software from [Arduino.cc](http://arduino.cc/en/Main/Software)

Once you have that, you need to plug the FTDI into your computer to find out what you need to do tto fixup any driver issues with talking to serial tty devices.

Windows 7 needs to use drivers that come with the arduino software.

Linux needs to set your user as permitted to talk to tty and dialout.


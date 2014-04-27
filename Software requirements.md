# Basic requirements

## Hardware

In addition to the Magnolia, you're going to need a 5V happy LED. A lot of 3V+ LEDs can handle the 5V from an arduino, but lower voltage ones tend to shine bright and short when powered up. It's best if you prepare an LED with a 100Ohm resister in series (tied to one leg). You're going to need a push button switch of some sort, a high value 2kOhm-2MOhm resistor, and for later lessons there will be a need for other components.

* a whole bunch of LEDs
* resistors (100Ohm, 2kOhm and 4kOhm)
* prototyping board (optional, but really useful) and jumper cables.
* 8-bit shift register
* photoresistor (light sensitive resistor)
* hobby servo
* piezo or other low resistance speaker

## Software

You're going to need to download and install the arduino IDE software from [Arduino.cc](http://arduino.cc/en/Main/Software)

Once you have that, you need to plug the FTDI into your computer to find out what you need to do tto fixup any driver issues with talking to serial tty devices.

Windows 7 needs to use drivers that come with the arduino software. If they are not installed correctly on first attempt, then try these steps.
* open windows device manager
* look for FTDI / USB Serial / FTRS232 something like that with a warning icon
* reinstall the driver, browse to where arduino installed (C:\program files (x86)\arduino\drivers\\...)
* Sometimes you will need to do this for two devices, not just the one, and the second one doesn't turn up until the first one has working drivers.

Linux needs to set your user as permitted to talk to tty and dialout.
* sudo usermod -a -G dialout <username>
* sudo usermod -a -G tty <username>


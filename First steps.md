# First steps

We're going to take one of the example sketches that comes with the arduino software and adjust it to match the Magnolia. The main thing to take from this lesson is that there is no pin 13 on the Magnolia, only analog pins, namely A0 - A5.

Basic setup
----------

Set up your magnolia by connecting the FTDI to the board, then connect the USB cable to the FTDI thingy.

Take an LED and stick the legs in GND and VCC. Take note of what the LED looks like, and which way round it goes, they only work one way round. Normally, the long leg is positive, or anode. Inside the casing, you can see the larger part is attached to the shorter leg (the big metal inside is the negative or cathode).

You're now ready to pull those legs apart and put the positive (anode) into one of the unmarked slots on the Magnolia. The slots without legend (markings) are the same as the analogue input pins on a regular Arduino. A0 is the pin nearest the markings for GND and VCC, A5 is the other end.

    GND VCC A5
    GND VCC A4
    GND VCC A3
    GND VCC A2
    GND VCC A1
    GND VCC A0

If you drop the anode into A0 and the cathode into one of the GND pins (any, they are all the same), then the LED should not be lit up (unless it's blinking, in which case someone has already set up the A0 blink sketch on this board)

Modifying an example
----

Now to the coding. Open up the arduino IDE, then open the blink example `file` > `examples` > `01.basics` > `blink` and look for the line:
    int led = 13;
and change the `13` to `A0`. After this, the sketch should now be able to blink your LED. You need to upload it.

Uploading a sketch
-----

The Arduino IDE has two round buttons (one a tick, the other an arrow) for checking your code, and uploading your code. This sketch should compile fine, so no need to check it compiles (especially as it will do it as part of the upload anyway) but something you do need to do is tell it what type of arduino you're using.

from the `tools` menu, select the `board` that matches yours. In this case the `Arduino Duemilanove w/ ATmega328`. Once you've done this you won't need to change the board unless you get another and different Arduino.

Hit the upload button (the arrow), and you should see the IDE compiling, then when it hits uploading, you should see the lights on your FTDI / Magnolia light up as the program is transferred to the chip. Once the upload is complete, the LED should start to blink on and off.
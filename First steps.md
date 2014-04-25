# First steps

We're going to take one of the example sketches that comes with the arduino software and adjust it to match the Magnolia. The main thing to take from this lesson is that there is no pin **13** on the Magnolia, only analog pins, namely **A0** - **A5**.

Basic setup
----------

Set up your magnolia by connecting the FTDI to the board, then connect the USB cable to the FTDI thingy.

Take an LED and stick the two legs in **GND** and **VCC**. It should light up. If not, try it the other way around.

Take note of what the LED looks like, and which way round it goes, they only work one way round. Normally, the long leg is positive, or *anode*. Inside the casing, you can see the larger internal part (the base) is attached to the shorter leg. The big metal inside is the negative or *cathode*.

You're now ready to pull those legs apart a bit and put the positive (anode) into one of the unmarked slots on the Magnolia. The unmarked slots are the same as the analogue input pins on a regular Arduino. **A0** is the pin nearest the markings for **GND** and **VCC**, **A5** is at the other end.

If you hold up your Magnolia board with the FTDI and USB cable off to the right, then this grid is the names of the 3x6 holes on the left side of the board.

    +-----------------------------+
    |GND VCC A5 +----------------+|
    |GND VCC A4 |  ATMega328     ||
    |GND VCC A3 +----------------+| -> FTDI
    |GND VCC A2                   |
    |GND VCC A1      Magnolia     |
    |GND VCC A0        Board      |
    +-----------------------------+

If you drop the anode into **A0** and the cathode into one of the **GND** pins, then the LED should not be lit up

## Modifying an example

Now to the coding. Open up the arduino IDE, then open the blink example `file` > `examples` > `01.basics` > `blink` and look for the line:
    int led = 13;
and change the `13` to `A0`. After this, the sketch should now be able to blink your LED. You need to upload it.

## Uploading a sketch

The Arduino IDE has two round buttons (one a tick, the other an arrow) for checking your code, and uploading your code. This sketch should compile fine, so no need to check it compiles (especially as it will do it as part of the upload anyway) but something you do need to do is tell it what type of arduino you're using.

from the `tools` menu, select the `board` that matches yours. In this case the `Arduino Duemilanove w/ ATmega328`. Once you've done this you won't need to change the board unless you get another and different Arduino.

Hit the upload button (the arrow), and you should see the IDE say that it is compiling, then when it hits uploading, you should see the lights on your FTDI / Magnolia light up as the program is transferred to the chip. Once the upload is complete, the LED should start to blink on and off with a one second delay.

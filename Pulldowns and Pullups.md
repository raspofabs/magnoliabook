# Pulldowns and Pullups

You've just finished the Buttons less and you're still not getting what the resistor thing was all about. Okay, this is for you.

## Circuits and potential difference

Start by thinking of **A0** as being able to read the voltage difference between **GND** and whatever is plugged into it. If you plug a jumper between **GND** and **A0**, it's going to read 0v. The reason is simple, the potential difference between **GND** (0v) and **GND** (0v) is 0v.

If you have a multimeter, imagine that **A0** is the red probe, and **GND** is the black probe.

When you call `digitalRead(...)`, the ATMega328p is checking if the voltage is over 3v. If it is, then you get a positive result from the call.

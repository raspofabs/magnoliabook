# Serial output

When something goes wrong, you need to debug it. Because the Arduino sketches aren't running on your PC, it's generally impossible to use a debugger, but you can still trace the cause of unexpected behaviour in your Magnolia by printing text back to your computer by making it talk to you over the cable. This lesson introduces the Serial Monitor, and how to add output to your sketch.

## Code setup

Before you can communicate, the Magnolia needs to know the way in which it will do the communication. On a Magnolia, just like an Arduino proper, the only thing we need to do is tell `Serial` to `begin`, and how fast it should communicate. Open the blinkA0 sketch again, and add to your `setup()`

    Serial.begin(9600);

And any time you start the sketch, the Magnolia will know to talk back to your FTDI, and in turn your PC, at a *baud rate* of 9600. That is, 9600 bits per second. That's plenty fine for most simple debugging.

To test it out, add to your `loop()`

    Serial.println("Test");

And then upload.

You should see that every two seconds (after the LED has done a cycle), the RX light flashes on the FTDI / Magnolia board. Now open up the Serial Monitor. It's `tools` > `serial monitor`, and as long as it is set to 9600 baud, you should start to see some output.

## Forms of output

`Serial` has a lot of different functions to output data.
DEC, HEX, println, print, write.

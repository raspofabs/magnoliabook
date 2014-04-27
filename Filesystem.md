# Filesystem

The ATMega328p doesn't have a hard drive attached, and even plugging in an SDCARD is a small project of its own, but the little microcontroller does have a very small amount of storage in the form of EEPROM, Electronically Erasable, Programmable Read-only memory. 512 bytes to be precise.

We can use this to store something that is meant to survive across power outages. We will use it to store the number of times the Magnolia has been booted up. Useless, but a good starting point for any ideas you might have as it includes reading and writing.

## The code

Reading and writing from EEPROM isn't a basic feature of Arduino, so you need to include a header that makes this code compilable. Add this at the top.

    #include <EEPROM.h>

We've still got to display something, so use the normal LED output code.

    int led = A0;

    void setup()
    {
        pinMode(led,OUTPUT);

but we're going to do the body of our code in setup this time, so after setting the pinmode, add this.

        int address = 0;
        int bootCount = EEPROM.read(address);
        EEPROM.write(address, bootCount+1);

        LEDFlash(bootCount);

        // wait for ten seconds, then reset the bootcount
        delay(10000);
        EEPROM.write(address, 1);
        LEDFlash(4);
    }

LEDFlash isn't an Arduino function, it's one we're going to write. Above the function setup, add this.

    void LEDFlash( int n )
    {
        for( int i = 0; i < n; ++i )
        {
            digitalWrite(led, HIGH);
            delay(50);
            digitalWrite(led, LOW);
            delay(200);
        }
    }

Now we have a function we can call. You can use this function in other sketches by copy pasting it in.

We're not going to use the loop on this sketch, so make sure it looks like this.

    void loop()
    {
    }

Now, when you upload, the first thing it will do is flash the number of times the magnolia has been powered up. Leave it for ten seconds, then it should flash again saying it's reset the boot count. Each time you unplug the USB and plug it back in again, then number of times it flashes should go up by one. Try it a few times to make sure. It doesn't matter how long you leave it unplugged, as EEPROM doesn't change when there is no power to the device.

## Take away

There is a place to store data that you need between power failures, but it's very limited, only 512 bytes. That's not enough for a desktop icon (they are normally at least 4k).

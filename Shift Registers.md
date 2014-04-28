# Shift Registers

To get around the limitations of the Magnolia's 6 IO pins, this lesson will show how to use shift registers to turn three pins into eight. This can be extended to many more outputs with shift registers that can be chained.

The shift register we are going to use is called the **HC595**, and the one in your kit is specifically an **SN74HC595** (normal one with legs so you can stick it in the prototyping board.)

    Qb  1   U   16 Vcc
    Qc  2       15 Qa
    Qd  3       14 SER
    Qe  4       13 OE(ground to enable)
    Qf  5       12 RCLK
    Qg  6       11 SRCLK
    Qh  7       10 SRCLR(power to disable)
    GND 8        9 Qh'

## The code

The **HC595** has a 16 pins, we will be using the eight output pins that are meant to be the parallel output to power our LEDs. To drive those outputs we will be connecting to the data and clock line for the internal registers, and pushing the internal registers to the output pins with the register clock.

When using chips with clock lines, we usually find they are triggered by positive-edge. This means the line transitions from a `LOW` to a `HIGH`. We'll start by adding this function to the top of our sketch so the main code can call it.

    void trigger( int pin )
    {
        digitalWrite(pin,HIGH);
        digitalWrite(pin,LOW);
    }

Inside the **HC595**, there are internal registers that can either be set high, or low. The internal registers ar called Qa' through Qh'. The external registers are called Qa through Qh. When **RCLK** is triggered, the values of the external registers are overwritten by the internal ones. This means we can safely modify the values on the internal registers without worrying that anything is happening outside.

To modify the internal registers, we need to use **SER** and **SRCLK**. Every time the **SRCLK** is triggered, two things happen: The values in Qh' down to Qb' get overwritten by Qg' down to Qa', and then the value of **SER** is read, shunted into Qa'. This is why it is called a shift register. Every time you trigger **SRCLK** all the values are shifted along to the next Q' register.

To shift out all eight values, we need a function to push one value out.

    void put_one( int val )
    {
        // set SER
        digitalWrite(SER, val);

        // trigger a shift
        trigger(SRCLK);
    }

This sets the **SER** line, then triggers the **SRCLK**, meaning the values get shifted. At this point, the outputs Qa - Qh are still in whatever state they were in before, but Qa' - Qh' have been shifted.

Often we will use binary to feed into shift registers, so we will do that and write a function to take a byte (8 bits) and set all the shift register values in sequence, then trigger **RCLK** to update the Q registers (the external ones.)

    void send_out( int bits )
    {
        for( int i = 0; i < 8; ++i )
        {
            // send only the lowest bit
            put_one( val & 1 );

            // move the next highest bit down
            val >>= 1;
        }
        trigger(RCLK); // move Q' into Q
    }

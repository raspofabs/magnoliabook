# Multiple Inputs

Shift registers come as input types as well as output types. To get more inputs than six into your Magnolia, whilst reducing the number of pins used to do it, we use a shift-in register, or a parallel to serial convertor.

The basic function of the shift-in register is the same as the shift register, the master (Magnolia) triggers the serial clock to shift the registers inside the chip. In both these chips, one pin can push data into the chip. In the shift-in register, there are three output pins, but we're not going to use all three, think of them as being convenient optional additions.

In the shift-register, we had a latch pin that when triggered, took the internal registers Q' and put them out to the external registers Q. In the shift-in register, we have internal registers Q, and when we trigger the latch pin, the external registers P overwrite them.

In this way, we can request the input pins are put into the internal buffer (Q), and then read each pin at our leisure (triggering the **SERCLK** to request the next value.)

## The code

## Wiring

## More inputs

Just as with shift registers, we can chain shift-in registers. As mentioned at the start of this lesson, both chips have serial input, and that means that you can tie **Q8** to **SER** on the next chip down. Make the **SERCLK** common, and the same with **PAR**, and you have all you need to run 16 inputs with the same number of IO pins from the Magnolia.

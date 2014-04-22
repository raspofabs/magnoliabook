# Buttons

To make interactive things, you need inputs. The most basic of which is a simple push button. This lesson shows you how to add a button, read its value, and react to it. In addition, we're going to learn an important lesson about circuits.

Firstly, we again start with the modified blink sketch. We will modify the first section:

    int led = A0;
    int button = A1;

We don't really need to modify the `setup()` section, as Arduino sets all pins to `INPUT` by default, but if it didn't we would do this:

    pinMode(led, OUTPUT);
    pinMode(button, INPUT);

Then we will modify `loop()` to react to our button press:

    if( digitalRead(button) )
    {
        digitalWrite(led, HIGH);
    }
    else
    {
        digitalWrite(led, LOW);
    }

`if( ... )` is a keyword that tells the processor that it should do the thing following if the value is not zero, else do the thing in the else. In this case, the `digitalRead` makes the processor set the led to on or off based on the value of the pin `button`.

Wiring
-----

You now need to wire up your Magnolia so the button is connected to **A1**. To do this, you will need to put your switch on a prototype board, and connect jumper wires from the **VCC** and **A1** to the two legs of the switch.

Uploading and seeing something strange
-----

When you upload the program, you will notice that the LED turns on before you touch the button. Sometimes it will flicker on and off a few times, but if you press the button, the LED will stay on constantly. This is because the switch connects the **VCC** to **A1** when the button is pressed, but there is nothing connected to **A1** when the button is not pressed. In this state, reading values from **A1** is very nearly random. Sometimes the voltage goes high just because moving your hand near the button increases the capacitance of the wire. Try playing with it for a bit before we fix the problem.

Fixing a floating input
------

When you want a wire to go high when a button is pressed, you need to connect the input of the button to the **VCC**, and the output of the button to **A?**, but you also need to connect **A?** to the **GND** so that when the button isn't pressed, the **A?** pin is *dragged down* towards **GND**.

Try changing the wire currently going from **A1** to the button so that it goes from **A1** to **GND**. Now, the LED stays off all the time.

If we connected the output side of the button to **GND** the LED would stay off while the button wasn't pressed, but as soon as we pressed the button, it would short the whole thing out and we could even break stuff.

The solution is to make te **GND** connected to the output side of the button, but in such a way that it doesn't matter if we press the button. To do this, we add a rather high valued resistor. Usually, anything over 2kOhms will do, I prefer 470kOhm just to be sure I'm not wasting juice on the *pulldown resistor*.

So, you wire up the circuit **VCC** to button in, button out to **A1**, but also button out, via *pulldown resistor* to **GND**. Now, when you run the program, the LED does not turn on randomly.

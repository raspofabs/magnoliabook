# Analogue Input

Often there will be a need for reading a value that isn't just `LOW` or `HIGH`, but something in between. Temperature, light level, humidity, or pressure, all come in a more continuous form than just yes and no. The Magnolia makes a decent enough sensor setup because all its pins are set up for reading analogue values.

## Analog reading

Before we get to the code, an important thing to remember. Unlike digitalRead and digitalWrite, the analogueRead doesn't use `LOW` and `HIGH`, but a range from values from `0` to `1023`, so make sure to keep that in mind.

## The code

We're going to be doing a nice and reactive example that uses a potentiometer. Set up a pin for the pot middle pin like this.

    int led = A0;
    int pot = A1;

    void setup()
    {
        pinMode(led, OUTPUT);
    }

Notice we don't set up the input pin. By default, all ATMega328P pins are in input state. You can do it explicitly if you wish (add `pinMode(pot, INPUT);` to `setup()`).

Then we need to read the value before we use it in the loop function. Note that value is a *local* variable, that is, it is created every time the loop function is called. With local variables, we have to explicitely initialise them. In this case, we declare the variable `value` as an `int` then give it a value from `analogRead` straight away.

    void loop()
    {
        int value = analogRead(pot);

        // turn the light on for a bit
        digitalWrite(led,HIGH);
        delay( 10 );

        // off time depends on value
        digitalWrite(led,LOW);
        delay( value );
    }

Note, the smaller `value` is, the shorter the delay, and this the faster the LED will flash.

## Wiring

We need to wire up the LED for output, and the potentiometer for input. Like with the button, we're going to ground the input line, but this time in different way.

Put the potentiometer in the board and temporarily give the legs names **PLEFT**, **PMID** and **PRIGHT**.

* **PLEFT** to **VCC**
* **PRIGHT** to **GND**
* **PMID** to **A1**
* **GND** to LED cathode (neg)
* **A0** to LED anode (pos)

## Running

Now try the example. The LED light should be flashing. If you turn the knob, the amount of time the LED is on for per cycle will change. Move the knob towards the left pin, and the `analogRead` will return a smaller value, around 0, so the light will be on most of the time. Turn the knob towards the right pin, and `analogRead` will return a large value, around the maximum of 1023, and the delay will cause the led to blink about once a second.

## Why three wires?

This is how we make inputs work with potentiometers (sliders and knobs, and other variable resistors). We ground one side, power the other, then catch a voltage off the middle pin.

What's really happening is that the potentiometer is acting as a dynamic pair of resistors, and they are doing a voltage division. This means that they are splitting the voltage between them by how much resistance each side of the middle pin has. The middle pin acts as a pointer to a continuum of different voltages between the left and right legs. When the middle is all the way over one side, that side has very little resistance, so ends up taking up a very small amount of the voltage. Meaning the middle has a value very similar to the side it is nearest to.

## Take away

Always ground things that are going to be used as inputs.

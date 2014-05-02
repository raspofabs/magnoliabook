# Analogue Input

Often there will be a need for reading a value that isn't just `LOW` or `HIGH`, but something in between. Temperature, light level, humidity, or pressure, all come in a more continuous form than just yes and no. The Magnolia makes a decent enough sensor setup because all its pins are set up for reading analogue values.

## Analog reading

Before we get to the code, an important thing to remember. Unlike digitalRead and digitalWrite, the analogueRead doesn't use `LOW` and `HIGH`, but a range from values from `0` to `1023`, so make sure to keep that in mind.

## The code

We're going to be doing a nice and reactive example that uses the photoresistor. Set up a pin for the resistor like this.

    int led = A0;
    int photo = A2;

    void setup()
    {
        pinMode(led, OUTPUT);
    }

Then we need to read the value before we use it in the loop function.

    void loop()
    {
        int value = analogRead(photo);

        // turn the light on for a bit
        digitalWrite(led,HIGH);
        delay( 10 );

        // off time depends on value
        digitalWrite(led,LOW);
        delay( value );
    }

Note, the smaller `value` is, the shorter the delay, and this the faster the LED will flash.

## Wiring

We need to wire up the LED for output, but also the photoresistor for input. Like with the button, we're going to ground the input line, but this time for a slightly different reason. Voltage across resistors is based on their resistance, and we will use that to make the input pin receive a differing voltage over different brightness reaching the photoresistor. First we wire up, then explain.

Put the photoresistor in the board and temporarily give the legs names **PH0** and **PH1**. Add a 2kOhm resistor to the board. Name the resistor legs **R0** and **R1**.

* *The resistor value is quite important, make sure it's around the 2000 Ohm range for this wiring up. (your kit has a 2k7Ohm)*
* **VCC** to **PH0**
* **PH1** to **R0**
* **PH1** to **A1**
* **R1** to **GND**
* **GND** to LED cathode (neg)
* **A0** to LED anode (pos)

## Running

Now try the example. The LED light should be flashing. If you cover the photoresistor, the amount of time the LED is on for per cycle will increase.

## Why ground?

If we ground with different values of resistor, the photoresistor will become sensitive to different levels of light. High value resistances make it less sensitve, allowing for sunlight levels. Low value resistances make it more sensitive, meaning you can detect low light level differences. This is because the grounding resistance pairs with the photoresistor resistance to create a voltage divider.

This is how we make inputs work with potentiometers (sliders and knobs, and other variable resistors). We ground one side, power the other, then catch a voltage off the middle pin.

If you have a unpredictable analogue input (such as a photoresistor) you can add a variable resistor to the mix so you can tweak the lower and upper range, effectively giving you a hardware trimming. To do this, attach **VCC** to the live end of the variable resistor, and then attach the **R1** to the middle pin of the variable resistor. This way you can adjust the resistance opposing the photoresistor to fine tune the sensitivity.

## Take away

Always ground things that are going to be used as inputs.

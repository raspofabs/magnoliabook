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

In a circuit, the current is the same the whole circuit around, but the voltage on the other hand, is not. Voltage is a measurement of potential difference, and a really obvious example is how we can add multiple batteries in a line to increase the voltage.

Two 1.5v batteries in a battery holder turn into a 3v battery because the voltages add up, but it's not like they have become two 3v batteries by touching, they are still two seperate 1.5v batteries than can still be tapped for power independently as well.

As two 1.5v batteries add up to 3v, so do two sources of resistance. We calculate what the voltage is at each resistance by dividing the voltage into two different ones based on the resistance of the two sources of resistance. In our circuit, the **GND** is 0v, and the **VCC** is 5v. To calculate the voltage between the two resistors, we can work it out from first principles and ohms law. Or we can just use this formula:

    middle volts = R2 / ( R1 + R2 ) * overall volts

Here, R2 is the 2k resistor, and R1 is the photoresistor. If R1 is very high (when it is dark, the photoresistor can measure in the megaohm range,) then R2 / (REALLY HIGH + R2) is going to be a very small value. If R1 is very low, then R2 / (almost zero + R2) is going to be almost 1.

This is how we make inputs work with potentiometers (sliders and knobs, and other variable resistors). We ground one side, power the other, then catch a voltage off the middle pin.

If you have a unpredictable analogue input (such as a photoresistor) you can add a variable resistor to the mix so you can tweak the lower and upper range, effectively giving you a hardware trimming. To do this, attach **VCC** to the live end of the variable resistor, and then attach the R2 to the middle pin of the variable resistor. This way you can adjust the value of R2 to fine tune the mid range.

## Take away

Always ground things that are going to be used as inputs.

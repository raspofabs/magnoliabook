# Photoresistors

Light levels can be measured in many ways. The cheapest is by using a photoresistor. Like a resistor, the photoresistor doesn't have a way round, so it's easy to add to a circuit. The resistance of a photoresistor changes dependent on the amount of light landing on its sensor area (the top side between the wire bits).

The resistance value ranges from hundreds of Ohms in bright sunlight, to millions of Ohms in complete darkness. This change in resistance is due to the light *exciting* the atoms in the gap between the wires, and when they are excited, they let electrons move across them. The brighter it gets, the less sticky the mud.

## The code

We can use exactly the same code we used for the potentiometer.

## Wiring

We need to wire up the LED for output again, but now we are going to use the photoresistor for input. Voltage across resistors is based on their resistance, and we will use that to make the input pin receive a differing voltage over different brightness reaching the photoresistor. First we wire up, then explain.

Put the photoresistor in the board and temporarily give the legs names **PH0** and **PH1**. Add a 2kOhm resistor to the board. Temporarily imagine the resistor legs have the names **R0** and **R1**.

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

If you have a unpredictable analogue input (such as a photoresistor) you can add a variable resistor (potentiometer will work) to the mix so you can tweak the lower and upper range, effectively giving you a hardware trimming. To do this, attach **VCC** to the live end of the variable resistor, and then attach the **R1** to the middle pin of the variable resistor. This way you can adjust the resistance opposing the photoresistor to fine tune the sensitivity.

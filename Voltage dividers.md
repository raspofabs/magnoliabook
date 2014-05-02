# Voltage dividers

Because the `analogRead` function returns a value based on the voltage going into the pin, the circuit we made with the photoresistor was set up to give **A0** a different voltage based on the light level. To do this, we used a voltage divider.

## Voltage and potential difference

In a circuit, the current is the same the whole circuit around, but the voltage on the other hand, is not. Voltage is a measurement of potential difference, and a really obvious example is how we can add multiple batteries in a line to increase the voltage.

Two 1.5v batteries in a battery holder turn into a 3v battery because the voltages add up, but it's not like they have become two 3v batteries by touching, they are still two seperate 1.5v batteries than can still be tapped for power independently as well.

As two 1.5v batteries add up to 3v, so do two sources of resistance. We calculate what the voltage is at each resistance by dividing the voltage into two different ones based on the resistance of the two sources of resistance. In our circuit, the **GND** is 0v, and the **VCC** is 5v. To calculate the voltage between the two resistors, we can work it out from first principles and ohms law. Or we can just use this formula:

    middle volts = R2 / ( R1 + R2 ) * overall volts

Here, R2 is the 2k resistor, and R1 is the photoresistor. If R1 is very high (when it is dark, the photoresistor can measure in the megaohm range,) then R2 / (REALLY HIGH + R2) is going to be a very small value. If R1 is very low, then R2 / (almost zero + R2) is going to be almost 1.

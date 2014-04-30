# Servos

If we need to make something be in a particular position based on some code, such as the rudder of a boat, the steering angle of a car, the openness of a window, or the direction of a solar panel, then we can use a servo.

Servos provide a way to request a position from 0 - 180 degrees. The request is done using only one IO pin, so you can control up to six servos with the Magnolia without adding any other chips.

## The code

No biggie for this one, just open up the example sketch found in `File` > `Examples` > `Servo` > `Sweep`

Change the pin the servo is attached to by changing this:

    myservo.attach(9);

to this

    myservo.attach(A0);

Now you can upload and wire it up.

## Wiring

Servos have leads with three wires. One is **GND**, one is **VCC**, and the last is the signal wire, **SIG**.

* connect servo **GND** to **GND**
* connect servo **VCC** to **VCC**
* connect **SIG** to **A0**

As soon as you connect **VCC**, the servo will probably squeak. When powered, the servo will try to go to wherever it thinks it should for a moment, and that could be anywhere while it is powering up.

As soon as you connect **SIG** to **A0**, the servo should rush to wherever it is meant to be, then continue to follower the 0 - 180 - 0 degree sweep that the Magnolia is looping through.

## Where to go?

You could try combining the light sensor lesson with the servo, and have the servo react to light levels.

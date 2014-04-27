# Multiple lights

Adding more is the next step. We're going to go over what you need to do to modify and extend an Arduino sketch.

## The code

reopen and modify the blink sketch like you did in lesson 1 if you have shut down the IDE, then where it now says

    int led = A0;

you need to add more lines:

    int led = A0;
    int led2 = A1; // second LED
    int led3 = A2; // third LED

and you need to set the pin mode for where we're going to connect the LEDs, so go to `void setup()`, and modify it.

    pinMode(led, OUTPUT);
    pinMode(led2, OUTPUT);
    pinMode(led3, OUTPUT);

and finally you need to modify the content of `void loop()` from this:

    digitalWrite(led, HIGH);
    delay(1000);
    digitalWrite(led, LOW);
    delay(1000);

to this:

    digitalWrite(led, HIGH); // turn on LED1
    delay(1000);
    digitalWrite(led, LOW); // then turn it off
    digitalWrite(led2, HIGH); // and turn on LED2
    delay(1000);
    digitalWrite(led2, LOW); // then turn it off
    digitalWrite(led3, HIGH); // and turn on LED3
    delay(1000);
    digitalWrite(led3, LOW); // then turn it off

Notice we don't add a delay between setting `led` to `LOW` and setting `led2` to `HIGH`. This is because we want the second LED to light up as soon as the first one has gone out, making it look like the light is moving from one LED to another.

## Wiring

Add another two LEDs with their anodes (positive legs) in **A1** and **A2**. Upload the sketch and you should see the three LEDs light up in sequence.

## The take-away

Whenever you add a new output to your sketch, you need to make sure you set the `pinMode` for the pin you are going to be using. Usually, you want to setup some `int` values for the pins so it is a little easier to know what each pin is for. You have to use `digitalWrite` to set whether the pin is outputting a **GND** (`LOW`) or **VCC** (`HIGH`) value.

## Finally

We're limited to only having 6 LEDs when powering them directly from the pins. There are a number of different ways around this limit, but the one we will be exploring later involves adding another chip to the setup, a shift register, and that will let us power 8 (or even more) LEDs from only three pins.

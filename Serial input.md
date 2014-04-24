# Serial input

Sometimes you need to command the Magnolia to do something from the PC. If you do, then Serial input is a great simple way to communicate with the board without using up any of the pins.

## Code setup

Just like in writing, before you can communicate, the Magnolia needs `Serial.begin()` to be called.

Instead of `Serial.write` we're going to call `Serial.read`, which returns either a character, or -1 if there is nothing to read.

To test it out, add this to your `loop()`

    int inchar = Serial.read();
    if( inchar != -1 )
    {
        Serial.print( "Recvd [" );
        Serial.print( inchar );
        Serial.print( "] = \"" );
        Serial.write( inchar );
        Serial.println( "\"" );
    }

And then upload.

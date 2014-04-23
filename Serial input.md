# Serial input

Sometimes you need to command the Magnolia to do something from the PC. If you do, then Serial input is a great simple way to communicate with the board without using up any of the pins.

## Code setup

Just like in writing, before you can communicate, the Magnolia needs `Serial.begin()` to be called.

Instead of `Serial.write` we're going to call `Serial.read`, which returns the number of bytes (characters) read into the space you gave it.

To test it out, add to your `loop()`

    char inBuffer[32] = {0};
    int bytesRead = Serial.read(inBuffer,32);
    Serial.print( "Recvd [" );
    Serial.print( inBuffer );
    Serial.print( "]" );
    Serial.print( bytesRead );
    Serial.println( "bytes" );

And then upload.

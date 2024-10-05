TASCAM RC-10 as IR control
===========================

This is a replacement for a TASCAM RC-10 remote control running on
Arduino via IR sending LED

Protocol
--------

The RC-10 communicates over a 2.5mm stereo headphone plug. The tip is
the signal from the remote control to the device under control (such as
an audio recorder), the ring is 3.3V DC from the device, and the sleeve
is ground.

The protocol is standard TTL-level UART (mark is 3.3V, space is 0V)
running at 9600 baud, 8 data bits, even parity, and 1 stop bit.

Here comes in handy an IR Receiver with a 56 kHz carrier frequency:
The 	TSOP4856 can run on 2.5V and is able to transport the 9600 baud.
So we only need to modulate the carrier frequence on top of the already
done work here to the serial output.
The receiver only needs to be soldered to a 2.5mm TRR jack.

The RC-10 sends a start byte when a button is pressed, a repeat byte
every 100ms afterward while the button is held down, and an end byte when
the button is released. The lower 5 bits of the byte is the command,
while the upper 2 bits indicate whether it's a start, repeat, or end
byte. A start byte has bit 7 set and bit 6 cleared, a repeat byte has
both bits 7 and 6 set, and an end byte has both bits 7 and 6 cleared.

Button command values
---------------------

| Button  | Value |
|---------|-------|
| Stop    |     8 |
| Play    |     9 |
| Record  |    11 |
| Forward |    14 |
| Back    |    15 |
| Mark    |    24 |
| F1      |    28 |
| F2      |    29 |
| F3      |    30 |
| F4      |    31 |

Note: F3 is marked (+) and F4 is marked (-).

Features
--------

This replacement software also supports a "turbo" mode which increases
the repeat rate of buttons to 2x the normal rate. This is useful for
impatient people. :) Turbo mode can be toggled with a press of the turbo
button.

License
-------

Copyright 2016 Christopher Williams. All Rights Reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

1. Redistributions of source code must retain the above copyright
   notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in
   the documentation and/or other materials provided with the
   distribution.

3. The name of the author may not be used to endorse or promote
   products derived from this software without specific prior written
   permission.

THIS SOFTWARE IS PROVIDED BY CHRISTOPHER WILLIAMS "AS IS" AND ANY
EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE,
EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

Acknowledgments
---------------

Special thanks to user iamin on www.ghielectronics.com for posting
information about the RC-10 protocol.
(See https://www.ghielectronics.com/community/codeshare/entry/1062)

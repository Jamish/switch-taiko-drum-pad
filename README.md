# Notes
See https://github.com/shinyquagsire23/Switch-Fightstick

Things I did, installing on Linux Mint:
1. Edit makefile to set `MCU = atmega32u4` for use with Arduino Micro
2. Download LUFA library, extract and rename to `lufa`,  and drop in same directory as this project. There should be a `lufa/LUFA` folder.
3. Install gcc-avr
 * https://www.pjrc.com/teensy/gcc.html
4. Run `make`
5. Follow https://github.com/shinyquagsire23/Switch-Fightstick#compiling-and-flashing-onto-the-arduino-micro to flash Joystick.hex
 * I got an error, `SerialException: Error touching serial port '/dev/ttyACM0'.`.  Fixed by running `sudo chmod a+rw /dev/ttyACM0` 
 * I had to be very fast to CTRL+A and CTRL+C the avrdude command from the console output. There was too much output and the console cleared the scrollback. I captured my command in `flash`

Next steps... define some input pins, and hook up some buttons. Let's hope the latency is good enough for Taiko Drum Master!

Here's how I figured out how to set the pins:
* https://medium.com/@jrejaud/arduino-to-avr-c-reference-guide-7d113b4309f7
* https://www.arduino.cc/en/Hacking/PinMapping

# World of Final Fantasy XP Auto-Grinder

A fork of a fork of a fork, modified to grind XP in a specific location in World of Final Fantasy, to level my character past level 60, so I can max out a few things in the game.

See previous projects for some more detailed information / setup process.

---

LUFA has been included as a git submodule, so cloning the repo like this:

```
git clone --recursive git@github.com:bertrandom/snowball-thrower.git
```

will put LUFA in the right directory.

Now you should be ready to rock. Open a terminal window in the `snowball-thrower` directory, type `make`, and hit enter to compile. If all goes well, the printout in the terminal will let you know it finished the build! Follow the directions on flashing `Joystick.hex` onto your Teensy, which can be found page where you downloaded the Teensy Loader application.

#### Thanks

Thanks to https://github.com/bertrandom/snowball-thrower for the updated information which modifies the original script to throw snowballs in Zelda. This C Source is much easier to start from, and has a nice object interface for creating new command sequences.

Thanks to Shiny Quagsire for his [Splatoon post printer](https://github.com/shinyquagsire23/Switch-Fightstick) and progmem for his [original discovery](https://github.com/progmem/Switch-Fightstick).

Thanks to [exsilium](https://github.com/bertrandom/snowball-thrower/pull/1) for improving the command structure, optimizing the waiting times, and handling the failure scenarios. It can now run indefinitely!

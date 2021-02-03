# About

This project provides code for a custom controller for "Taiko no Tatsujin: Drum 'n' Fun!" for Nintendo Switch (a.k.a., Taiko Drum Master).

## The Circuit
The controller is powered by an Arduino Micro, with four arcade buttons hooked up to pins D2, D3, D4, and D5. Each button has one terminal hooked up to the digital input pin, and the other terminal hooked up to the ground pin on the Arduino Micro. There are no external resistors needed, since we take advantage of the Arduino Micro's built-in 

## Button Mappings & Usage

Arcade buttons hooked up to pins D2 and D3 map to "Left Don" and "Right Don", which are the red notes (striking the middles of the taiko drum)

The buttons hooked up to pins D4 and D5 map to "Left Ka" and "Right Ka", which are the blue notes (striking the left/right edges of the taiko drum)

Most interfaces are navigable. There is currently no pause button to exit songs early, and you cannot navigate the game modes or options, but you can just use a different controller for that. From title screen to playing any song you'd like in the regular mode, you can do it all with just these 4 buttons. 

When you play with this, just select the normal "Pro Controller" input with the default button controls. You can use Left Ka and Right Ka to cycle back/forwards in menus, including character selection, song selection, and difficulty selection. You use Right Don for the "B" button to cancel selections, and Right Ka for the "A" button to confirm selections.

I'm still testing out latency, but I'm able to hit perfects pretty consistently, so I think latency is fine!

# Four Forks 
This is a fork of a fork of a fork of a fork...

@progmem reverse engineered the HORI Switch Fightstick's USB interface, then @shinyquagsire23 forked it and added some nicer button definitions in order to auto-print some Splatoon 2 posts, then @bertrandom forked it in order to send pre-defined inputs to throw perfect snowballs in Breath of the Wild, then @kidGodzilla forked it to grind in World of Final Fantasy, and then I forked it and modified it to take button inputs from the Arduino Micro's digital pins and convert them to Switch button presses.

# Installation & Notes
See https://github.com/shinyquagsire23/Switch-Fightstick for very detailed notes on setting up the LUFA library, setting up the AVR tools, and flashing the Arduino Micro. This is bare-metal code on the Arduino Micro, and therefore we don't use Arduino's IDE for anything other than copy/pasting the initial 
 
Here are my personal notes that I followed; I used Linux Mint personally:
1. Edit makefile to set `MCU = atmega32u4` for use with Arduino Micro
2. Download LUFA library, extract and rename to `lufa`,  and drop in same directory as this project. There should be a `lufa/LUFA` folder.
3. Install gcc-avr
 * https://www.pjrc.com/teensy/gcc.html
4. Run `make`
5. Follow https://github.com/shinyquagsire23/Switch-Fightstick#compiling-and-flashing-onto-the-arduino-micro to flash Joystick.hex
 * I got an error, `SerialException: Error touching serial port '/dev/ttyACM0'.`.  Fixed by running `sudo chmod a+rw /dev/ttyACM0` 
 * I had to be very fast to CTRL+A and CTRL+C the avrdude command from the console output of the Arduino IDE. There was too much output and the console cleared the scrollback. I captured my command in `flash`, after which I could just double-click the reset button and run `./flash` to update my micro controller.

Latency is good enough for Taiko Drum Master! 

Here's how I figured out how to set the pins:
* https://medium.com/@jrejaud/arduino-to-avr-c-reference-guide-7d113b4309f7
* https://www.arduino.cc/en/Hacking/PinMapping

# The rest of the README.md is the original README.md of the project I forked.

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

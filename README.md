Adafruit-Retrogame
==================

Raspberry Pi GPIO-to-USB utility for classic game emulators.

How-to: http://learn.adafruit.com/retro-gaming-with-raspberry-pi

Pre-built version supports the default pin/key mapping shown in the tutorial. For other layouts, edit retrogame.c.

Retrogame2PlayersPi2
===================

Raspberry Pi GPIO-to-USB utility for classic game emulators.

Compilation
===========

````
$ git clone https://github.com/ian57/Recalbox-Retrogame-2Players-Pi2
$ cd Recalbox-Retrogame-2Player-Pi2
$ make
````

Pinout Mapping
==============

````
	GPIO 02 ->  KEY_0         // HotKey Player1
	GPIO 03 ->  KEY_9         // HotKey Player2
	GPIO 04 ->  KEY_UP        // UP Player1
	GPIO 17 ->  KEY_DOWN      // DOWN Player1
	GPIO 27 ->  KEY_LEFT      // LEFT Player1
	GPIO 22 ->  KEY_RIGHT     // RIGHT Player1
	GPIO 10 ->  KEY_1         // START Player1
	GPIO 09 ->  KEY_5   		  // COIN/SELECT Player1
	GPIO 11 ->  KEY_R   		  // UP Player2
	GPIO 05 ->  KEY_F    		  // DOWN Player2
	GPIO 06 ->  KEY_D   		  // LEFT Player2
	GPIO 13 ->  KEY_G   		  // RIGHT Player2
	GPIO 19 ->  KEY_2   		  // START Player2
	GPIO 26 ->  KEY_6   		  // COIN/SELECT Player2
	GPIO 14 ->  KEY_Z   		  // BUTTON5/TL Player1
	GPIO 15 ->  KEY_SPACE  	  // BUTTON2/X Player1
	GPIO 18 ->  KEY_LEFTSHIFT // BUTTON4/Y Player1
	GPIO 23 ->  KEY_X         // BUTTON6/TR Player1
	GPIO 24 ->  KEY_LEFTCTRL  // BUTTON1/A Player1
	GPIO 25 ->  KEY_LEFTALT   // BUTTON2/B Player1
	GPIO 08 ->  KEY_E     		// BUTTON5/TL Player2
	GPIO 07 ->  KEY_Q     		// BUTTON3/X Player2
	GPIO 12 ->  KEY_W       	// BUTTON4/Y Player2
	GPIO 16 ->  KEY_T     		// BUTTON6/TR Player2
	GPIO 20 ->  KEY_A     		// BUTTON1/A Player2
	GPIO 21 ->  KEY_s     		// BUTTON2/B Player2
````

Maintaining Start P1 + Coins/Credits P1 more than 1 seconds will produce "KEY_ESC" (Escape Key).

Installation
============

Now we have configure to allow retrogame to work and be launched at startup. As in http://learn.adafruit.com/retro-gaming-with-raspberry-pi/buttons, you make

Retrogame requires the uinput kernel module. This is already present on the system but isn't enabled by default. For testing, you can type:

````
sudo modprobe uinput
````

To make this persistent between reboots, append a line to /etc/modules (or edit the file) :

````
sudo sh -c 'echo uinput >> /etc/modules'
````

Now we're in good shape to test it! Retrogame needs to be run as root (need access to memory), i.e.:

````
sudo ./retrogame
````

Give it a try. If it seems to be working, press control+C to stop the program and we'll then set up the system to launch this automatically in the background at startup.

````
sudo nano /etc/rc.local
````

Before the final "exit 0" line, insert this line:

````
/home/pi/Recalbox-Retrogame-2Players-Pi2/retrogame &

````
If you placed the software in a different location, this line should be changed accordingly. "sudo" isn't necessary here because the rc.local script is already run as root.

Reboot the system to test the startup function:

````
sudo reboot
````

The software will now be patiently waiting in the background, ready for use with any emulators.

Each emulator will have its own method for configuring keyboard input. Set them up so the keys match your controller outputs. Up/down/left/right from the arrow keys is a pretty common default among these programs, but the rest will usually require some tweaking.

Arcade Wiring
=============

See https://github.com/ian57/Recalbox-Retrogame-2Players-Pi2/wiki




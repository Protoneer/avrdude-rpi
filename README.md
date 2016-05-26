Using avrdude with the Raspberry Pi
===================================

Since the Raspberry Pi lacks a DTR pin that makes it oh-so-easy to upload your hex files into
the avr, we need this hack to make it just as easy.  When you wire up your atmega chip, be sure
to connect one of the digital gpio pins to the reset pin, and then you'll be able to use avrdude
as if your serial cable actually had a dtr pin.

Instructions:
-------------

Install using script:

    $ git clone https://github.com/Protoneer/avrdude-rpi ~/avrdude-rpi && ~/avrdude-rpi/install



Modify the autoreset script to use the pin that you wired up to the reset pin.  See the line in
autoreset where we do "pin = 11" and change the 11 to your gpio pin number.

Now when you run avrdude from anywhere (including via arduino's normal UI) it will flag dtr when
it is about to upload hex data.

To upload to ATmega328 @ 8Mhz:

    $ avrdude -v  -c arduino -p ATMEGA328P -P /dev/ttyAMA0 -b 38400 -U flash:w:sketch_name.hex

To upload to ATmega328 @ 16Mhz: 

    $ avrdude -v -c arduino -p ATMEGA328P -P /dev/ttyAMA0 -b 115200 -U flash:w:sketch_name.hex

http://www.deanmao.com/2012/08/12/fixing-the-dtr-pin/
https://github.com/openenergymonitor/avrdude-rpi

Make sure Python is installed:

    $ sudo apt-get update
    $ sudo apt-get install python-dev
    $ sudo apt-get install python-rpi.gpio

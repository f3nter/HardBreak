# Bus Pirate 5

## Theory

The Bus Pirate 5 is an updated version of the original[ Bus Pirate](bus-pirate.md), which was discontinued. The new version was released in January 2024 and is major leap forward, with much faster speeds, more supported protocols, higher power handling, and better firmware support. If you need a more modern, high-performance tool, Bus Pirate 5 is the better choice. However, Bus Pirate v3.6 is still usable for basic hacking and lower-speed applications.

### Features

* Based on Raspberry Pi Foundation RP2040 with 128Mbit flash storage
* 1.65-5volt operating range, 3 states with voltage measuring on every pin
* Programmable 1-5.0volt output / 0-500mA current limit
* 1Gbit NAND flash storage
* 320 x 240 pixel LCD display
* Live voltage measurements
* Visable pinout on display for every mode
* basic logic analyzer integrated (upto 62.5MSPS)
* 1-Wire, I2C, SPI, UART, MIDI, serial LEDs supported

## Setup

{% tabs %}
{% tab title="Linux" %}
```bash
sudo minicom -D /dev/ttyUSB0 -b 115200
sudo picocom -b 115200 -r -l /dev/ttyUSB0
```

Plug in your Bus Pirate and change _/dev/ttyUSB0_ accordingly. (You can use `dmesg` to verify the port of the Bus Pirate)
{% endtab %}

{% tab title="Windows" %}
You can use[ Tera Term](https://en.wikipedia.org/wiki/Tera_Term) to open a Terminal Window and connect to the Bus Pirate (baudrate=115200).
{% endtab %}
{% endtabs %}

### TODO



## Resources

[Buspirate - Hompage](https://buspirate.com/)

# DSMR_reader_schematic_PCB
This repository contains a schematic and PCB layout for a dutch ESMR/DSMR smart meter reader via the P1 port. Key features are:
- Based on wemos d1 mini (ESP8266, 1M FLASH)
- inverted serial port using BC547 transistor
- Power can be taken from the smart meter or from an external source (both 5V input), selectable via a jumper
- telegram readings from the P1 port can be controlled through a GPIO output that is connected to the data request pin via an opto-coupler
- You can also read a water meter through an inductive pulse sensor. The PCB also has room for a small SX1308 boost DC-DC convertor as some of these need a voltage higher than 5V
- While i was at it: connections to add other switches, buttons and sensors such as a PIR, 1-wire, serial, I2C. So in fact you could even use the PCB for completely different purpose than smart meter reading....

Note: this is my first repository on github so pelase bare with me....more details to be added later

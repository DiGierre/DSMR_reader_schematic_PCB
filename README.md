# DSMR_reader_schematic_PCB
This repository contains a schematic and PCB layout for a dutch ESMR/DSMR smart meter reader via the P1 port. Key features are:
- Based on wemos d1 mini (ESP8266, 1M FLASH)
- inverted serial port using BC547 transistor
- Power can be taken from the smart meter or from an external source (both 5V input), selectable via a jumper
- telegram readings from the P1 port can be controlled through a GPIO output 

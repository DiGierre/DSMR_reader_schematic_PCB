# DSMR_reader_schematic_PCB

Note: this is my first repository on github so please bare with me....more details to be added later

![alt text][logo]
[logo]: Schematic_DSMR_reader_only_PCB_v1.0.png

This repository contains a schematic and PCB layout for a dutch ESMR/DSMR smart meter reader via the P1 port. Key features are:
- Based on wemos d1 mini (ESP8266, 1M FLASH)
- inverted serial port using BC547 transistor
- Power can be taken from the smart meter or from an external source (both 5V input), selectable via a jumper
- telegram readings from the P1 port can be controlled through a GPIO output that is connected to the data request pin via an opto-coupler
- You can also read a water meter through an inductive pulse sensor. The PCB also has room for a small SX1308 boost DC-DC convertor as some of these need a voltage higher than 5V
- While i was at it: connections to add other switches, buttons and sensors such as a PIR, 1-wire, serial, I2C. So in fact you could even use the PCB for completely different purpose than smart meter reading....


For code to run on the wemos D1 mini ESP8266 I'll refer you to the following links:

[CustomP1UartComponent](https://github.com/nldroid/CustomP1UartComponent "CustomP1UartComponent by nldroid") by nldroid. This uses the [ESPhome](https://esphome.io/index.html) framework. I have not tested this yet myself but likely will in the near future, as I am planning to start using more ESPhome and also want to combine this firmware with the pulse reader fo the water meter. Note you will need to change the pin for the data request to D7 - the CustomP1UartComponent is using D5.

Another build for P1 smart meter readings is from [this](https://willem.aandewiel.nl/index.php/2019/04/09/dsmr-logger-v4-slimme-meter-uitlezer/) site from Willem Aandewiel (warning: Dutch only). The code and more is also on his [Github](https://github.com/mrWheel/DSMRloggerWS).

I'm current running this firmware (version 1.0.4) and it's running quite stable since November last year. In any case proof that the PCB seems working fine. I have a FSMR5 meter and I'm powering the PCB from the 5V inside the smart meter (Did you know by the way this is free? - Yes really, the built-in smart meter power supply is not metered and delivers 5V / 250mA)



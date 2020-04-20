# DSMR_reader_schematic_PCB

Note: this is my first repository on github so please bare with me....more details to be added later

![alt text](Schematic_DSMR_reader_only_PCB_v1.0.png "Smart meter P1 port reader schematic")

This repository contains a schematic and PCB layout for a dutch ESMR/DSMR smart meter reader via the P1 port. Key features are:
- Based on wemos d1 mini (ESP8266, 1M FLASH)
- inverted serial port using BC547 transistor
- Power can be taken from the smart meter or from an external source (both 5V input), selectable via a jumper
- telegram readings from the P1 port can be controlled through a GPIO output that is connected to the data request pin via an opto-coupler
- You can also read a water meter through an inductive pulse sensor. The PCB also has room for a small SX1308 boost DC-DC convertor as some of these need a voltage higher than 5V
- While i was at it: connections to add other switches, buttons and sensors such as a PIR, 1-wire, serial, I2C. So in fact you could even use the PCB for completely different purpose than smart meter reading....


![alt text](DSMR5_reader_PCB_top.PNG "Smart meter P1 port reader PCB top side")

The schematic as shown above only shows the parts relevant for the smart meter reader. It consists of a serial port convertor, data request circuit and the wemos. The circuit is essentially designed to work for ESMR5 meters. I have a Sagemcom XS210 which is ESMR5. It may wotk for other smart meters but you may have to tweak. Some older DSMR/ESMR meters do not have a power supply and/or can only deliver less power, some do not have the inverted serial port or may have outputs that are not isolated through and opto-coupler.

Usage:
The circuit can be fed from the 5V in the smart meter or by an external power supply. By default it will take power from the meter. If you want to power it externally then short-circuit JP1. However this connects the external 5V to the meter's 5V so in that case do not use a 6-pin but 4-pin cable or make sure your meter does not deliver 5V. Else 2 power supply will be connetced together and that's generally bad practice.

The smart meter can deliver 250 mA and this will not be enough for the ESP during peak load. Hence I put a fairly large capacitor on the input, C2. I am using a low ESR elco (low internal resistance) of 1500uF. Do note that I have read reports that some meter deal poorly with the large elco as it has a high peak current power up and the current protection of the meter kicks in and for some meters does not recover. 

By default the circuit will use the data request pin via the opcocoupler PH11 circuit, which converts the 3v3 from GPIO D7 to 5V using the smart meter's 5V. When high (5V on Data request), the meter sends telegrams via the serial port each second until low again. If you don't want to use this then short-circuit JP2 (put a cap on the pins or simply solder a wire). I don't recommend this since it may load the ESP as it needs to handle serial traffic each second and particularly if you also want to have it do other stuff this may cause instability.


For code to run on the wemos D1 mini ESP8266 I'll refer you to the following links:

[CustomP1UartComponent](https://github.com/nldroid/CustomP1UartComponent "CustomP1UartComponent by nldroid") by nldroid. This uses the [ESPhome](https://esphome.io/index.html) framework. I have not tested this yet myself but likely will in the near future, as I am planning to start using more ESPhome and also want to combine this firmware with the pulse reader fo the water meter. Note you will need to change the pin for the data request to D7 - the CustomP1UartComponent is using D5.

Another build for P1 smart meter readings is from [this](https://willem.aandewiel.nl/index.php/2019/04/09/dsmr-logger-v4-slimme-meter-uitlezer/) site from Willem Aandewiel (warning: Dutch only). The code and more is also on his [Github](https://github.com/mrWheel/DSMRloggerWS). I'm current running this firmware (version 1.0.4) and it's running quite stable since November last year. In any case proof that the PCB seems working fine. I have a FSMR5 meter and I'm powering the PCB from the 5V inside the smart meter (Did you know by the way this is free? - Yes really, the built-in smart meter power supply is not metered and delivers 5V / 250mA)



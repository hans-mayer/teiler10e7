# teiler10e7

( english: divider by 10^7 )

This is part of a NTP project.

It contains a PCB ( printed circuit board ) designed with EAGLE 7.7.0

The NTP server exist of the following components

* a Banana Pi M1 with GNU/Linux 3.4.108
* a rubidium 10 MHz frequency standard
* a frequency divider by 10000000 to get a 1PPS

This PCB has 2 connectors.

* JP1 connected to the GPIO of the Banana Pi
* JP2 connected to the rubidium 10 MHz frequency

Connector JP1

* GPIO0 pin 11 BCM17 - input for 1PPS
* GPIO2 pin 13 BCM27 - output to insert pulses
* GPIO3 pin 15 BCM22 - output for delay
* GND - pin 6,9,14,25
* Vcc +3.3 V - pin 1,17

The 10 MHz signal - a sine wave with about 10 Vss - is converted into TTL with a schmitt trigger 74HC132D. 7 stages of decade counters (74HT390D) will produce a 1PPS. After the first stage (1 MHz) there is a NAND and a X-OR. This allows to adjust the timer especially after boot. The NAND is connected with the other pin to GPIO3 and offers the possibility the strip off some pulses. This results in a delay. With the X-OR additional pulses can be inserted. It's connected to GPIO2.

A detailed description will come soon.


![circuitdiagram.png](/circuitdiagram.png)

This is the finished PCB 

![pcb_teiler.png](/pcb_teiler.png)



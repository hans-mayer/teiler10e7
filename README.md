# teiler10e7

( english: divider by 10^7 )

This is part of a NTP project.

It contains a PCB ( printed circuit board ) designed with EAGLE 7.7.0

The NTP server exist of the following components

* a Banana Pi M1 with GNU/Linux 3.4.113
* a rubidium 10 MHz frequency standard
* a frequency divider by 10000000 to get a 1PPS ( this hardware )

This PCB has 2 connectors.

* JP1 connected to the GPIO of the Banana Pi
* JP2 connected to the rubidium 10 MHz frequency

Connector JP1

* GPIO0 pin 11 BCM17 - input for 1PPS
* GPIO2 pin 13 BCM27 - output to insert pulses
* GPIO3 pin 15 BCM22 - output for delay
* GND - pin 6,9,14,25
* Vcc +3.3 V - pin 1,17

The 10 MHz signal - a sine wave with about 10 Vss - is converted into TTL with a schmitt trigger 74HC132D. 7 stages of decade counters (74HT390D) will produce a 1PPS signal. After the first stage (1 MHz) there is a NAND and a X-OR. This allows to adjust the timer especially after boot. The NAND (IC3D) is connected with pin 12 to GPIO3 and offers the possibility the strip off some pulses. This results in a delay. With the X-OR (IC4A) additional pulses can be inserted on pin 1. It's connected to GPIO2.

To manage inserting and stripping off pulses I wrote a small C program which can be found here: https://github.com/hans-mayer/wiringPin

A detailed description will come soon.


![circuitdiagram.png](/circuitdiagram.png)

This is the finished PCB (component site) <br>
The soldering site has only the connector JP1

![pcb_teiler.png](/pcb_teiler.png)

This is the same but on my breadboard before I developed the PCB with Eagle. 

![breadboard](/breadboard.png)

See also:

[//]: # * [Stratum-1 NTP Server with rubidium source](http://blog.mayer.tv/2017/06/11/stratum-0-server.html){:target="_blank"}
[//]: # * [Banana Pi - GPIO - WiringBP](http://blog.mayer.tv/2016/01/08/bananapi-gpio-wiringbp.html){:target="_blank"}
[//]: # * [failed first attempt with 74HC4059](http://blog.mayer.tv/2016/01/01/cd47hc4059.html){:target="_blank"}

<a href="http://blog.mayer.tv/2017/06/11/stratum-0-server.html" target="_blank">Stratum-1 NTP Server with rubidium source</a>
<a href="http://blog.mayer.tv/2016/01/08/bananapi-gpio-wiringbp.html" target="_blank">Banana Pi - GPIO - WiringBP</a>
<a href="http://blog.mayer.tv/2016/01/01/cd47hc4059.html" target="_blank">failed first attempt with 74HC4059





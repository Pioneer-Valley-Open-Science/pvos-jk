---
author: Don
comments: true
date: 2013-04-28 23:18:54+00:00
layout: post
slug: open-lab-monitor-base-peripherals
title: 'Open Lab Monitor: Base + Peripherals'
wordpress_id: 54
---

After chatting with Craig, Jake, and Ben over the last 24 hours, we decided to try a different configuration for the Open Lab Monitor (OLM).  Instead of having ethernet on-board the 'main' Open Lab Monitor, we designed a version that is really just a "Jeenode minus a radio" -- that is, an Arduino Uno-compatible board that will need an FTDI cable to be programmed via a PC -- plus our own, custom "OLM" port interface.

Here's a picture of the board schematic and layout so far:

[![OLM-base_v0.2](http://www.pvos.org/wp-content/uploads/2013/04/OLM-base_v0.2-276x300.png)](http://www.pvos.org/wp-content/uploads/2013/04/OLM-base_v0.2.png) [![OLM-base_v0.2brd](http://www.pvos.org/wp-content/uploads/2013/04/OLM-base_v0.2brd1-186x300.png)](http://www.pvos.org/wp-content/uploads/2013/04/OLM-base_v0.2brd1.png)

Another very significant change: we added the Atmega328P's  "I2C" interface to the OLM ports. Each "OLM Port" is now a port for a 2x5 ribbon cable connector with (you guessed it) 2x5=10 pins -- namely:



	
  * A digital I/O pin capable of pulse width modulation (PWM)

	
  * An analog I/O pin;

	
  * power and ground pins;

	
  * the SPI bus:  MISO, MOSI, and SCK pins (if used, SPI will also rely on the digital I/O pin as the "chip select" pin);

	
  * the I2C interface: SDA and SCL pins;

	
  * A RESET pin.


Here's a closeup of one of the OLM "ports":

[![OLMport](http://www.pvos.org/wp-content/uploads/2013/04/OLMport-300x117.png)](http://www.pvos.org/wp-content/uploads/2013/04/OLMport.png)

This redesign both a) simplifies the "base" OLM board, making DIY construction of it easier (and cheaper), b) allows for two more "ports" on the base board, and c) opens up an entire class of new sensor devices: I2C devices, which are quite ubiquitous.  Exciting!

Because one of the first applications we have in mind is an ethernet-capable device that sends sensor readings to an online database, we've also now designed our first OLM "peripheral" -- an ethernet controller chip (the ENCJ2860) and ethernet jack (the same sold by Sparkfun).  The design allows for use of JeeLabs "Ethercard" library, a well-tested and actively maintained library with several nice examples available for the Arduino IDE.  The resultant "OLM Ethernet Peripheral" schematic is pictured here:

[![OLM-periph-ether_v0.2sch](http://www.pvos.org/wp-content/uploads/2013/04/OLM-periph-ether_v0.2sch-300x222.png)](http://www.pvos.org/wp-content/uploads/2013/04/OLM-periph-ether_v0.2sch.png)

And here's the board layout so far (cute, isn't it?):

[![OLM-perip-ether_v0.2brd](http://www.pvos.org/wp-content/uploads/2013/04/OLM-perip-ether_v0.2brd-94x300.png)](http://www.pvos.org/wp-content/uploads/2013/04/OLM-perip-ether_v0.2brd.png)



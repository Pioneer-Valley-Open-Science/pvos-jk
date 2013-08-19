---
author: Don
comments: true
date: 2013-04-27 18:14:53+00:00
layout: post
slug: open-lab-monitor-first-steps
title: 'Open Lab Monitor: First Steps'
wordpress_id: 42
---

![olm_throughhole](/assets/olm_throughhole.png)Todd and I spent a good deal of time yesterday figuring out the minimal viable version of the Open Lab Monitor (OLM) and putting it into a schematic.  We ended up choosing to emulate the very elegant and minimal design of the [JeeNode](http://jeelabs.net/projects/hardware/wiki/JeeNode), remove the JeeNode's radio (though wireless connectivity will soon be revisited!) and add ethernet connectivity.  Another important design decision was to select only through-hole components for the board: this will both facilitate our own learning process, and it also allows for the possibility of an easy-to-assemble kit for use in K-12 and university contexts.

So, what is the Open Lab Monitor?  It's essentially yet another take-off on the popular Arduino microcontroller platform, but tweaked slightly in order to make it easier to add peripherals that would be useful when making measurements in a scientific research context.  The main tweaks are the inclusion of some custom ports that can be connected to via some snug, cheap cables; our plan is to make a series of peripherals for this port interface that will allow for measuring temperature, humidity, moisture, pH, and do some simple electrochemistry.  The advantage of using an Arduino-based system is that doing so allows the user to connect to the incredible array of online tutorials that provide instructions for doing pretty much anything that a cheap microcontroller electronics platform allows; with minor modifications, the code from such projects should work on the Open Lab Monitor, as well.  We're also planning on designing a shield for the Raspberry Pi that would use the same custom connector interface, so that folks that would prefer to use the more powerful processor and operating system of the R-Pi can use the same inexpensive peripherals.  The decision as to whether to use an Arduino-based or R-Pi-based system is then mostly a matter of the user's comfort with the associated programming styles, as well as whether a low-power, battery-operated system is something they require (if so, then the Arduino is the way to go).

We're hoping to finalize this initial design in the next week or so, and make our first printed circuit boards soon.  Then we'll be in a better position to start designing the several peripherals we have in mind for this board.

Here's the schematic as it stands now:

![olmetherv02](/assets/olmetherv02.png)

Exciting times ahead!

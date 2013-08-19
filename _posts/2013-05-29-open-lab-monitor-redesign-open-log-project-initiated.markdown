---
author: Don
comments: true
date: 2013-05-29 20:36:38+00:00
layout: post
slug: open-lab-monitor-redesign-open-log-project-initiated
title: Open Lab Monitor Redesign; Open-Log project initiated
wordpress_id: 103
---


![olm-base_v0.9brd-300x189.png](/assets/olm-base_v0.9brd.png)

We got our first batch of [OLMs](https://github.com/dwblair/open-lab-monitor) in a few weeks ago -- but haven't yet had much time to play with them! Already, though, based on conversations about the applications we have in mind for these devices, we've decided to change the pin arrangements on the "OLM Connectors" -- so that now we'll be providing both SPI and I2C connections, as well as a directy VIN connection (to whatever power source is powering the board).

![arrival5.5](/assets/arrival5.5.jpg)

This new design fits nicely in a small, inexpensive plastic case from SERPAC.  Our plan over the next few weeks is to design a simple "ambient temp and humidity and probe temp" peripheral that will connect to the OLM main board via a ribbon cable, and to figure out what sorts of modifications to the SERPAC case will be required in order to allow for a nice, initial temperature-monitoring prototype.

![serpac](/assets/Screenshot-from-2013-05-29-162815-300x158.png)

**Open-log**.  Meanwhile, on the software front, we've initiated an "open data logging" project we're calling "[open-log](http://open-log.pvos.org/)".  It's based on [Flask](http://flask.pocoo.org/), and is very crude at this point (baby steps!), but we have plans to implement an server-based logging platform based on numpy, matplotlib, D3, and PyTables.  Feel free to [check out the code on github](https://github.com/dwblair/open-log) -- fork away!



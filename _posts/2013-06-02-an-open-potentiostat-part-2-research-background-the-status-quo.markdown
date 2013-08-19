---
author: Craig
comments: true
date: 2013-06-02 23:51:44+00:00
layout: post
slug: an-open-potentiostat-part-2-research-background-the-status-quo
title: 'An Open Potentiostat (Part 2): Research Background, The Status Quo'
wordpress_id: 119
---

I (Craig) have had some previous experience working with potentiostats (pstat) in my experimental physics PhD research (on proton and ionic charge transport in polymer membranes and non-aqueous liquids).  My opinion is entirely formed from one particular model, the [Solartron 1287](http://www.solartronanalytical.com/our-products/potentiostats/Model-1287A.aspx); it is a popular, electrochemical Swiss-army knife with a ton of features and a hefty price tag (~$10k).  My lab used this pstat along with another even more costly (~$20/30k) box, the Solartron 1252B/1260 Frequency Response Analyzer to do conductivity measurements using the technique of impedance spectroscopy.




As a naive software developer enthralled by the open source spirit of the Python language community, I wanted to automate my tedious materials conductivity characterization experiments.  This commercial instrument does offer computer control with a proprietary and pricey (~$2k) Windows only software package - but this was found to be very limiting for our purposes.  The alternative taken at the time was to utilize the set of low-level commands to replicate part of what their software was doing in an environment fully under my control.  Now, these two-letter bare-bones commands (text GPIB protocol) were listed with brief description in the manual, but that “documentation” was incredibly meager and woefully insufficient.  Luckily, I was able to reverse engineer the commercial program by spying on the computer to instrument communications.  After about of month of hacking, unravelling sequences of hundreds of commands, I finally had a working DIY impedance vs. frequency sweep program running within Python on a Linux system.  (Later, I found out from a Solartron rep. that their contracted out software development took 4 years with direct engineering staff access!)


![EIS_gen3](/assets/EIS_gen3.png)




_High throughput ion conducting materials characterization platform with homegrown Python software.  Center bottom: SI 1260 Impedance Gain/Phase Analayzer; center middle: SI 1287 Electrochemical Interface._


All the software was now free - too bad the hardware would set a lab back > $40k!  I was left with the sense that this commercial instrument technology was not only over-priced, but out-of-date, and maybe “user-friendly” but certainly not “developer-friendly”.  If the potential of the open source community could be harnessed into making scientific instruments, perhaps they wouldn’t make the most precise tools, but they’d definitely be more accessible.

---
author: Craig
comments: true
date: 2013-06-11 22:07:49+00:00
layout: post
slug: an-open-potentiostat-part-3-low-cost-diy-potentiostat-tear-down
title: 'An Open Potentiostat (Part 3): Low Cost DIY Potentiostat Tear-down'
wordpress_id: 129
---

While visiting Amherst, Don showed me a DIY low cost potentiostat that he was mailed by [Dr. Jack Summers](http://wcu.academia.edu/JackSummers), a chemistry professor at Western Carolina University, and fellow [PublicLab](http://www.publiclab.org/) member.  We thought it would be a perfect starting point on which to base our design of an electrochemical toolkit / peripheral for the [OLM](http://www.pvos.org/?p=54), so we began reverse engineering it.

![](https://lh5.googleusercontent.com/IAsWAk7Wy_1jExNPLe4KGyVjrnBwoncJeW_2yRF-pptM-Hs3IGM49510U4aNL7SZ0yPwxIkWcp2-HjjDjZgAzk3ANdNlQxa9u-TBeVgWcwZ4SOv67NvYf9WB)    ![](https://lh3.googleusercontent.com/uL3gS6WZHOUntePbx_VK6lYvhNdaqeyEtjye3b8Y40wW9kECB-LcbvN75dvPBp58pSTwzVUQpjWIW9lUkAeOy1NqQdeqgj9ZETtmps2_o9mux0FCz2hyGizK)    ![](https://lh3.googleusercontent.com/JZ3arik8FsLhnu1Cij057C_QK3AqAP06GWuGtHPaZB0hrbBU4x-PPcHXptNqsDthFnxvRdxrWAOtV5xWe9OwYa9dBHzB-U6YBZwtJ4JB7QEVCnQmGPyE-JcQ)


On the outside, it appears to be a homemade USB gadget with a nifty retro look in its VHS case.  We note the labelled standard three probes - “working”, “reference”, and “counter” - with convenient alligator clip leads. Featured on the otherwise nondescript case is an “On/Off” switch (presumably to save energy in battery mode!), a multiposition powers of 2 “Gain” setting knob, and a continuous 10k potentiometer (not to be confused with “potentiostat”) “Offset” knob.  Inside we find a [Texas Instrument’s LaunchPad](http://www.ti.com/ww/en/launchpad/home_head.html?DCMP=Value_Line&HQS=launchpad), a  < $5 prototyping platform in the spirit of the Arduino (but not 100% compatible).  Stuffed in with the microcontroller board, are two analog electronics boards, the pair of knob controls, and a tangle of wires.  This instrument was designed to be used with these fairly inexpensive [patterned ceramic electrodes (Au and Pt) from Pine Instruments](http://www.pineinst.com/echem/viewproduct.asp?ID=46681) at $200 per 6pk ( although they sell even cheaper [screen-printed carbon electrodes](http://www.pineinst.com/echem/viewproduct.asp?ID=46564) at $30 per 10pk).  Since electrode materials and design are so important, maybe they will be the subject of future post (once we have a better clue).




We didn’t actually have the special electrodes at the time nor an experiment in mind; so, rather than plug it into a computer and try it out, Don and I decided to rip it apart (sorry Jack) to see what it was made of:


![](https://lh4.googleusercontent.com/c14oDyKFLV3HxfyUi5P28fdliHIDXd9YCtraMjj3X94RuirHugmmNdyVlXIsm8pL1qvO72d-8BNuzoSEizW_QPRgmekdK33qAFdn30DHLMX64MLyF8PxxlqX) ![](https://lh6.googleusercontent.com/_2B3ssubPAvfYYDfUS4ercTPeNlbzbihJnHVHdVLWnj53arJfCOqhOgt9qX2rKx7LgtBl2zuat2w6plBPvVuk7UaqHq_Gr5j73ADYjhYbkBziFuqNPa4BLEL)

![](https://lh4.googleusercontent.com/Gf9npCfQufzwjlqWP1dkbJLWs1GNjLcnxTCg8zq6R4pRA93vs3nlIHeo-g-dZrNzVLPcwYjKHsX5C_XTs3GMDSwVaeKxs7Z7Nxv5BhkZQZZ8qkFJLob1Eb8L)

The two analog boards have hand-drawn etched copper traces.  The smaller one prominently features a [TI DCH010512DN7](http://www.ti.com/product/dch010512d) DC-DC power converter module that boosts the USB’s 5V power up to a split +/- 12V using an oscillating amplifier and inductor - a pretty neat trick to get an expanded voltage range into small package.  The external electrolytic capacitors and resistors help to smooth the ripple and limit the current from this switching supply.  Also on this board is a _npn_ power transistor which is used to drive some sort of solution stirring motor (not included in our gift-package) with a digital trigger from the microcontroller.  The larger board accommodates circuitry centered around a 14 pin DIP IC, the [LM148J](http://www.ti.com/lit/ds/symlink/lm348.pdf) Quad op-amp; these are 4 separate general purpose amplifiers which use negative feedback techniques to generate and condition for measurement the voltage and current signals of the potentiostat.  The +/- 12V lines from the little board feed right into the supply pins of this op-amp chip.


Great, we now had some idea what we were dealing with - it was no longer just a magical black-box that does science.   Here is our fuzzy picture of what that critical IC component was doing:


![](https://lh3.googleusercontent.com/25D62hF_qfq36_Wsl215mH-6xILfROVZA4bCPJOjzZx5v8o4_TpNxMvFW8Y0wUcbvQMBD-Wjg6_3MNF6-p4Hfd2t3jtsAMuiV2pRD3TEtTEz19tPQDEVXGdI)

It was time for me to leave and return to Providence, fortunately Don let me take this baby with me so that I could continue to analyze its function and circuitry.  (We forgot the electrodes again....doh!)

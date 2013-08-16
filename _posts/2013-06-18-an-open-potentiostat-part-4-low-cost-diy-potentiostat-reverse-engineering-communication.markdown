---
author: Craig
comments: true
date: 2013-06-18 19:25:57+00:00
layout: post
slug: an-open-potentiostat-part-4-low-cost-diy-potentiostat-reverse-engineering-communication
title: 'An Open Potentiostat (part 4): Low Cost DIY Potentiostat Reverse Engineering
  - Communication'
wordpress_id: 136
---

When I got back to Providence, I first hit the books (well, just “[The Art of Electronics](http://www.amazon.com/Art-Electronics-Paul-Horowitz/dp/0521370957)”) to refresh myself of op-amp circuit design (alright, let’s not pretend that I ever once understood how they worked).   Then, I had the good sense just to plug the DIY pstat into a USB port and see if I could talk to it - it happened to be on a fresh install of Ubuntu 13.04.  After initial glimmers of success using `miniterm`, the connection became spotty. For good measure, I checked `dmesg`; here is what the kernel (3.8.0-19-generic) is thinking when it sees this new device:




    
    [83504.450100] usb 3-3.2: new full-speed USB device number 6 using xhci_hcd
    [83504.491003] usb 3-3.2: New USB device found, idVendor=0451, idProduct=f432
    [83504.491007] usb 3-3.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
    [83504.491010] usb 3-3.2: Product: Texas Instruments MSP-FET430UIF
    [83504.491013] usb 3-3.2: Manufacturer: Texas Instruments
    [83504.491015] usb 3-3.2: SerialNumber: CEFF426C50141C13
    [83504.491188] usb 3-3.2: ep 0x82 - rounding interval to 1024 microframes, ep desc says 2040 microframes
    [83504.496986] cdc_acm 3-3.2:1.0: This device cannot do calls on its own. It is not a modem.
    [83504.496991] cdc_acm 3-3.2:1.0: No union descriptor, testing for <span style="color: #000000; background-color: #ffff00;">castrated</span> device
    [83504.497008] cdc_acm 3-3.2:1.0: ttyACM0: USB ACM device
    [83514.535829] hid-generic 0003:0451:F432.0005: usb_submit_urb(ctrl) failed: -1
    [83514.535854] hid-generic 0003:0451:F432.0005: timeout initializing reports
    [83514.536081] hid-generic 0003:0451:F432.0005: hiddev0,hidraw3: USB HID v1.01 Device [Texas Instruments Texas Instruments MSP-FET430UIF] on usb-0000:00:14.0-3.2/input1




Eww.... what is that about being “castrated”?!  Anyway, I’ve found that these new version 3 kernels are very picky (and downright rude) about USB protocol.  I decided to try the “Serial Monitor” tool of the Arduino IDE since that is likely very similar to the TI IDE with which this instrument was developed.  Much better luck this time; here is the device’s response to me stupidly banging out newlines:




    
    Starting Voltage (mV-1800mV)
     <code>24648.00
     Ending Voltage (mV-1800mV)
     24648.00
     Scan Rate in mV/sec (sec)
     -2888
     Pre-concentration time (sec)
     -2888
     Mode (0:ASV, 1:CV)
     -38
     &</code>




Hmmm... those numbers are a little odd.  Oh right, I have the [source code](https://github.com/Pioneer-Valley-Open-Science/olm-pstat/blob/master/doc/src/Feb21_2013_ASV_CV_3.ino)!  I should be able to figure out how to operate it.  After staring at the code for a while, I realize I just have to enter the right numbers at each prompt (duh!)... but I also discovered a little white lie - the “CV” mode (the Cyclic Voltammetry mode I’m interested in) is actually number “2” not “1” and likewise “ASV” mode ( Anodic Stripping Voltammetry) is actually “1”!  It is so very useful for a scientist/hacker to have the source code of a scientific instrument.  Hastily, I put a 10k resistor between the working and counter electrodes and shorted the reference to counter in order to make a two-probe connection.  Then, I carefully entered the numbers with necessary zero-padding to ensure the right conversion...BOOM:




    
    Starting Voltage (mV-1800mV)
    1800.00
    Ending Voltage (mV-1800mV)
    0.00
    Scan Rate in mV/sec (sec)
    100
    Pre-concentration time (sec)
    1
    Mode (0:ASV, 1:CV)
    2
    &
    0.0355    0.0000
    0.0198    0.0000
    0.0216    0.0000
    [snip...]
    -0.2894    0.0015
    -0.2990    0.0002
    -0.3085    0.0024
    -0.3042    0.0067
    -0.3111    0.0033
    -0.3059    0.0072
    -0.3120    0.0241
    -0.3146    0.0152
    -0.3311    0.0180
    -0.3233    0.0245
    -0.3363    0.0191
    -0.3381    0.0428
    -0.3190    0.0326
    -0.3355    0.0441
    -0.3528    0.0478
    -0.3554    0.0684
    -0.3494    0.0695
    -0.3363    0.0693
    -0.3589    0.0847
    [snip...]
    -1.6584    2.7638
    -1.7861    2.7732
    -1.6523    2.7736
    -1.7687    2.7730
    -1.7071    2.7860
    -1.7496    2.7986
    -1.7019    2.7971
    -1.7210    2.8010
    -1.6923    2.8151
    -1.6949    2.8209
    -1.6940    2.8353
    -1.7496    2.8353
    -1.7210    2.8442
    -1.7357    2.8466
    -1.8313    2.8514
    -1.6914    2.8572
    -1.8052    2.8759
    -1.7844    2.8535
    -1.7444    2.8518
    -1.7192    2.8531
    -1.6714    2.8401
    -1.7905    2.8394
    -1.7661    2.8288
    -1.6732    2.8240
    -1.6932    2.8190
    -1.6819    2.8125
    -1.7314    2.7916
    -1.6662    2.7914
    -1.7470    2.7866
    -1.7210    2.7832
    -1.7131    2.7721
    -1.7071    2.7714
    -1.6940    2.7612
    [snip...]
    0.0328    0.0000
    *
    Starting Voltage (mV-1800mV)




(The full data set can be found [here](https://github.com/Pioneer-Valley-Open-Science/olm-pstat/blob/master/test/JSpstat_10k_2probe.csv).)




Granted, I have no idea what these numbers mean, so I copied and pasted them into a text file and plotted them in [IPython (“pylab” mode)](http://www.scipy.org/Getting_Started):




    
    In [1]: D = loadtxt("JSpstat_10k_2probe.csv", comments='#')
    In [2]: plot(D[:,0],D[:,1])
    Out[2]: [<matplotlib.lines.Line2D at 0x3d5ff10>]
    In [3]: title("Summers’ Group DIY Pstat - 10k Resistor, 2 probe")
    Out[3]: <matplotlib.text.Text at 0x3d5c990>
    In [4]: xlabel("Voltage?")
    Out[4]: <matplotlib.text.Text at 0x3d51210>
    In [5]: ylabel("Current?")
    Out[5]: <matplotlib.text.Text at 0x3d52350>
    In [6]: savefig("JSpstat_10k_2probe.pdf")




![](https://lh6.googleusercontent.com/I6LkKI_8V3hOAI3xeQbsvdBxBAurJpMTaWrNmIqJHLgkaPaJ04Bkuhfwapuar7oSVMLhzP6-NqBV9OaG71QoqXLg7NSZoykgLahNm4fjMBMgM8U69-iel0lr)




Seems reasonable, the current-voltage (I-V) response of a resistor should be a straight line according to Ohm’s law!

---
title: PIR Sensor Comparison
categories:
- projects
tags:
- passive infrared
- PIR
- sensor
- sparkfun
---
I recently started working on a project that <em>might</em> require some Passive Infra-red (PIR) sensors. <a href="http://www.sparkfun.com/">Sparkfun</a> had two different ones, so I figured I'd try them both.

{% include image.html
            img="images/wp/IMG_0932-640x426.jpg"
            title=""
            caption=""
            url="https://alvarop.com/images/wp/IMG_0932.jpg" %}

The comparison is between a <a href="https://www.sparkfun.com/products/9587">Zilog ePIR</a> and an <a href="https://www.sparkfun.com/products/8630">SE-10</a>. One very important thing to note is that I did not use the<strong> ePIR</strong>'s serial interface. I only used the hardware interface, set to the highest sensitivity, and shortest delay. I felt that this would be a better comparison. I made a video that shows my test setup, as well as some results, so most of the relevant information is there. I'll use this blog post to add some setup details, as well as my conclusion.

<iframe src="https://www.youtube.com/embed/xZGYn-oipQc" frameborder="0" width="640" height="360"></iframe>

First of all, I must warn everyone (as <a href="http://www.sparkfun.com/">Sparkfun</a> did) about the <strong>SE-10</strong>. The wire colors mean absolutely <strong>NOTHING</strong>. As you can see in the photo, there is a black, brown, and red cables. Here's what they were connected to on mine: <strong>Black</strong>=<strong>12V</strong>, <strong>Brown</strong>=<strong>GND</strong>, <strong>Red</strong>=<strong>Alarm</strong>. It's not a huge problem, just make sure you know before supplying power. There's a small label that says <strong>B+</strong> and <strong>AL</strong> on the bottom near each wire that should help.

The alarm pin needs to have a pull-up resistor, but that's about it. Out of the box, it worked without a problem.

You'll notice the <strong>SE-10</strong> takes in <strong>12V</strong>. Several comments on the <a href="http://www.sparkfun.com/">Sparkfun</a> product page deal with powering the device with <strong>5V</strong> or <strong>3.3V</strong>. All I did was remove the <strong>5V</strong> regulator and jump across it with a wire (big red one on the photo). Unfortunately, I ripped off some traces while attempting to remove the regulator (oops!). At first it wouldn't work, but I noticed a very small trace going under one of the resistors and connecting to the ground pin of the regulator. After connecting that to ground again (small red wire on the photo), everything worked fine at <strong>5V</strong>.

{% include image.html
            img="images/wp/IMG_0931-640x426.jpg"
            title="SE-10 Jumper"
            caption="SE-10 Jumper"
            url="https://alvarop.com/images/wp/IMG_0931.jpg" %}

The <strong>ePIR</strong> sensor took me a bit longer to get working. The datasheet is quite long, mostly documenting all the configurations and serial interface. They do have a nice schematic showing the <strong>Hardware Interface Mode.</strong> It shows all the connections required to get this working without the serial interface. The schematic has three potentiometers, a photoresistor and three regular resistors. Luckily, you don't even need that for the most basic operation. The pots are all for setting the <strong>delay</strong>(pin 2), <strong>sensitivity</strong>(pin 3), and <strong>light gate threshold</strong>(pin 6). You can just connect the <strong>delay</strong> and <strong></strong> sensitivity<strong> </strong>pins to ground, and the <strong>light gate </strong>to VCC(which is <strong>3.3V</strong> for this device). This will use the minimum delay (2 seconds), maximum sensitivity, and have the device always on.

The<strong> light gate</strong> is there in case you want to enable/disable your sensor depending on ambient light with a photoresistor. You can also just use the pin as an enable/disable for the whole device. It is disabled while the input is less than <strong>1V</strong>.

The<strong> delay</strong> had me a bit confused initially. It is not a delay before it lets you know something is moving. On the other hand, once it detects something, it holds a 'detected' state for the delay period. I had the minimum delay setting of 2 seconds (it goes up to 15 minutes), so after detecting motion, the signal would stay low for that amount of time.

So which sensor should you use? As always, it depends... I found the <strong>ePIR</strong> sensor to be much more sensitive than the <strong>SE-10</strong>. Maybe it was just the one I received, or maybe they're all like that, but the <strong>ePIR</strong> could detect me at a wider angle (and behind the blanket!). It also seemed faster than the <strong>SE-10</strong> at longer distances. On the other hand, when I stood a few feet in front of the sensors and turned around, the response was about the same.

Another thing I mentioned in the video is the 'delay' time with the <strong>ePIR</strong>. The output signal is much cleaner because of it. The<strong> SE-10</strong>, on the other hand, constantly switches while something is moving. I guess that could be useful if you're trying to count something...

If you're looking for a very easy to setup sensor, and aren't too worried about sensitivity, I'd go with the <strong>SE-10</strong>. It's three wires and a pull-up resistor! Doesn't get much simpler than that. On the other hand, if you want more control, and are willing to spend more time tweaking stuff, the <strong>ePIR</strong> is probably a better idea.

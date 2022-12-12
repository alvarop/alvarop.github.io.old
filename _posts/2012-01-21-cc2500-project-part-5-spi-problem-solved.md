---
title: CC2500 Project (Part 5) -- SPI Problem Solved!
categories:
- cc2500
- projects
tags: []
---
So I wrote last week about getting UART working on the MSP430G2533 but having major problems with the SPI interface... I was so frustrated that I caved in and purchased a <a href="http://www.saleae.com/logic/" target="_blank">Salae Logic</a> analyzer. It finally arrived today, and I had a chance to test it.

{% include image.html
            img="images/blgr/s640/IMG_7201.jpg"
            title="Salae Logic in action!"
            caption="Salae Logic in action!"
            url="/images/blgr/IMG_7201.jpg" %}

As soon as I opened the box, I connected it to sniff the SPI lines between my msp430 and cc2500 radio. It took me maybe 10-15 minutes to set up everything, including the Salae software to decode SPI on the fly. I ran my radio-setup code and observed the logic output. It seemed like something was happening, but it wasn't quite working.

{% include image.html
            img="images/blgr/s640/25331.png"
            title="First capture with msp430g2533"
            caption="First capture with msp430g2533"
            url="/images/blgr/25331.png" %}

To get a better idea as to what it should look like, I connected my msp430g2452, which had a working SPI link with the radio. The first thing I noticed was an error saying that the clock polarity was inverted. Aha! So the SPI clock on the 2533 was low when idle, while the specification says it's supposed to be high.So I went into the datasheet and figured out how to fix the clock problem.

{% include image.html
            img="images/blgr/s640/2452.png"
            title="'Correct' capture with the msp430g2452"
            caption="'Correct' capture with the msp430g2452"
            url="/images/blgr/2452.png" %}

I tried it again and, not surprisingly, it failed. Looking more carefully at the MISO/MOSI lines, I realized that they were backwards! Turns out that the SPI IO pins do not match between the msp4302533 and the 2452. I swapped two wires and everything started working!

While I was really happy I fixed the problem, this means that my previously mentioned PCB will only work with one of the two devices. My plan is to use the more expensive 2533 as a PC-to-radio bridge, since it has both a hardware UART to talk to the pc and hardware SPI to talk to the radio. The cheaper 2452 only has one SPI to use the radio.

{% include image.html
            img="images/blgr/s640/IMG_7202.jpg"
            title="Launchpad with cc2500 Radio and Salae logic"
            caption="Launchpad with cc2500 Radio and Salae logic"
            url="/images/blgr/IMG_7202.jpg" %}

In the end, I'm still happy. The Salae logic was extremely helpful and easy to use. It took me less than an hour to solve a problem I hadn't figure out in two days! Now I will be able to focus much more time in coming up with good radio libraries, instead of debugging silly problems.


---
title: Beginnings of Home(ok, apartment) Automation
categories:
- automation
- cc2500
- projects
tags: []
---
I've been neglecting my projects for a while, but I finally decided to stop being lazy and started working on them again. Several of my old posts deal with msp430's and <a href="http://alvarop.com/category/cc2500/">cc2500's</a>, but they're mostly hardware updates and examples of changing lights to music. Now that I have a semi-stable platform and decent libraries, I figured I might as well do something useful with them.

My 'end goal' is to be able to control things like lighting and <a href="https://www.youtube.com/watch?v=lou5PjWXxgU">temperature </a>automatically(and/or remotely) as well as gather data about the environment(temperature, motion, air quality, etc.) As usual, the first thing I did was start designing the whole system in my head and over-complicating things. I wanted to do a fancy server with flexible communications protocols, which got overwhelming pretty fast. After some time without getting anything done, I decided to start fresh and do small, manageable, tasks that eventually will end up being the full working system.

The first task I decided to do was to get my beaglebone talking to my cc2500 radios. I didn't want to waste time trying to figure out how to get SPI and interrupts working on the beaglebone, so I went for the simpler solution and put an msp430 to control the cc2500. I say simpler because I already had a <a href="https://github.com/alvarop/msp430-cc2500/blob/master/projects/bridge/main.c">uart-to-msp430-to-cc2500</a> bridge working, so the only new thing was figuring out the uart on the beaglebone. Luckily, there are several <a href="http://www.jerome-bernard.com/blog/2012/06/04/beaglebone-serial-ports-and-xbees/">good posts</a> about it online.

{% include image.html
            img="images/wp/IMG_1333-640x426.jpg"
            title="Beaglebone with CC2500"
            caption="Beaglebone with CC2500"
            url="/images/wp/IMG_1333.jpg" %}

Once I had my 'server' talking to the radio, I had to write a program to control it. Again, I could write an entire, complicated, sever application, or I could do something <a href="https://github.com/alvarop/pc/tree/master/projects/swrite">much simpler</a> to start. Since I'm currently only testing with wireless lighting, I don't need the server to receive data. Instead of having an always running application that takes over the serial port, my <a href="https://github.com/alvarop/pc/tree/master/projects/swrite">swrite </a>program is called from the command line each time a new packet is sent. While limited, this solution is enough for now.

{% include image.html
            img="images/wp/IMG_1338-331x480.jpg"
            title="Wireless RGB LED Controller"
            caption="Wireless RGB LED Controller"
            url="/images/wp/IMG_1338.jpg" %}

To start testing the lighting control, I mounted two RGB LED strips with controllers in my apartment. One is behind my bike rack in the living room, and the other behind my bed. The one behind my bed will eventually be tied to my alarm clock, so I can start turning up the lights before I wake up. Since my computer is not in my room, I use the one in the bike rack for testing.

{% include image.html
            img="images/wp/IMG_1343-640x426.jpg"
            title="Lights on Bike Rack"
            caption="Lights on Bike Rack"
            url="/images/wp/IMG_1343.jpg" %}

So that's what I have so far. It's not terribly exciting, but maybe if I write about it, I'll be more motivated to keep working on it. Right now I'm writing a program on the server that will allow me to schedule events. A bit like <a href="http://linux.die.net/man/8/crond">crond</a>, but instead of running programs, it calls my own functions. The first test will be to set up the light-alarm. I hope it works!

{% include image.html
            img="images/wp/IMG_1349-640x426.jpg"
            title="RGB LED strip behind bed"
            caption="RGB LED strip behind bed"
            url="/images/wp/IMG_1349.jpg" %}

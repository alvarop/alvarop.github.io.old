---
title: USB Cable Tester
categories:
- projects
tags: []
---

Ever wonder if your USB C cable is USB2 or USB3? Do you have some charge-only cables hiding in a box just waiting for the right moment to spoil your project plans?!
Fear no more!

I’ve made a simple board to test most of the things!

{% include image.html 
	img="images/usb_cable_tester/1.jpeg" 
	title="USB Cable Tester v2.0 - Front"
	caption="USB Cable Tester v2.0 - Front"
	url="/images/usb_cable_tester/1.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/2.jpeg" 
	title="USB Cable Tester v2.0 - Back"
	caption="USB Cable Tester v2.0 - Back"
	url="/images/usb_cable_tester/2.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/3.jpeg" 
	title="USB Cable Tester v2.0 - Side"
	caption="USB Cable Tester v2.0 - Side"
	url="/images/usb_cable_tester/3.jpeg"
%}

(This post is derived from my original [twitter thread](https://twitter.com/alvaroprieto/status/1594036248481771520) about it.)

## How does it work?

Connect your cable to both sides and the signal LEDs will light up if they are connected. Here’s an example of a USB2 cable and a thunderbolt 3 cable.

{% include image.html 
	img="images/usb_cable_tester/4.jpeg" 
	title="Testing a USB-C 2.0 Cable"
	caption="Testing a USB-C 2.0 Cable"
	url="/images/usb_cable_tester/4.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/5.jpeg" 
	title="Testing a Thunderbolt 3 Cable"
	caption="Testing a Thunderbolt 3 Cable"
	url="/images/usb_cable_tester/5.jpeg"
%}

Want to test a USB A to C cable? How about a USB A to Micro B? USB C to B? Mini B? You’ve got it!

{% include image.html 
	img="images/usb_cable_tester/6.jpeg" 
	title="Testing a USB A to C Cable"
	caption="Testing a USB A to C Cable"
	url="/images/usb_cable_tester/6.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/7.jpeg" 
	title="Testing a USB C to B Cable"
	caption="Testing a USB C to B Cable"
	url="/images/usb_cable_tester/7.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/8.jpeg" 
	title="Testing a USB A to Micro B Cable"
	caption="Testing a USB A to Micro B Cable"
	url="/images/usb_cable_tester/8.jpeg"
%}

Here’s what a the dreaded charge-only cables look like. I had to make my own since I had previously banished them from my lab! (These are the real reason I made this)

{% include image.html 
	img="images/usb_cable_tester/9.jpeg" 
	title="Testing a Charge-only Cable"
	caption="Testing a Charge-only Cable"
	url="/images/usb_cable_tester/9.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/10.jpeg" 
	title="Homemade Charge-only Cable"
	caption="Homemade Charge-only Cable"
	url="/images/usb_cable_tester/10.jpeg"
%}

But….What if my cable is too short!? We have that covered too 😂

{% include image.html 
	img="images/usb_cable_tester/11.jpeg" 
	title="Testing a short USB 4 Cable"
	caption="Testing a short USB 4 Cable"
	url="/images/usb_cable_tester/11.jpeg"
%}

{% include image.html 
	img="images/usb_cable_tester/12.jpeg" 
	title="Testing a short USB 4 Cable (Part 2)"
	caption="Testing a short USB 4 Cable (Part 2)"
	url="/images/usb_cable_tester/12.jpeg"
%}

## How can I get one?!
Like most of my projects, the files are available on [the github repo](https://github.com/alvarop/usb_c_cable_tester) under an open hardware license.

If you want to make your own, I have instructions on ordering your own from JLCPCB here: [https://github.com/alvarop/usb_c_cable_tester/blob/main/ORDERING.md](https://github.com/alvarop/usb_c_cable_tester/blob/main/ORDERING.md)

## What do all the signals mean?!
I still need to make a nice diagram explaining what you should see for each type of cable. Until then, here's the short version:

All the signals from the USB A connector will show up on the right column of LED's (A1-A12). The "B" side is only used for the USB-C port on the left. The D+/D- signals are the "USB 2.0" data lines. USB-3 will have TX1+/- and RX2+/-.

Every USB-C cable _should_ have either CC1 or CC2 (which will change if you rotate the cable).

## Updates!
You can follow project updates on github. I've released a [new version](https://github.com/alvarop/usb_c_cable_tester/releases/tag/v2.1) with some fixes, but, unfortunately, it still has some issues.

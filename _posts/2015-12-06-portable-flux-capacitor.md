---
title: Portable Flux Capacitor
categories:
- projects
tags: [projects]
---

This year's work holiday party was Back to the Future themed. I didn't have any good costume ideas, so with a week to go, I decided to build a portable flux capacitor to bring instead.

<div align="center"><iframe width="640" height="360" src="https://www.youtube.com/embed/MZ-XaeUl97o" frameborder="0" allowfullscreen></iframe></div> 

<br />

The first thing I did was to order some [addressable RGB LED strips][0] online. 

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 1.jpg"
            title="First prototype"
            caption="First prototype"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 1.jpg" %}

I bought some clear tubing at the hardware store and cut the LED strips to size. I then used a [Teensy LC][1] that I got at the [Hackaday Superconference][2] with the FastLED library to start playing with the LEDs.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 7.jpg"
            title="Teensy-LC"
            caption="Teensy-LC"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 7.jpg" %}

My first attempt used cardboard for the front plate, but the clear tubing was stronger than I expected and did not like being bent that much. The tube would either pop out of its place or bend the cardboard.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 8.jpg"
            title="Behind the LED strips"
            caption="Behind the LED strips"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 8.jpg" %}

I had some leftover alder wood boards from other projects, so I decided to use that instead. It was just large enough to fit the tubes, about the right size for the box I had, and strong enough to hold everything in place.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 9.jpg"
            title="Full board from behind"
            caption="Full board from behind"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 9.jpg" %}

After making sure everything fit, I spray painted the board silver (because that's the only color I had.)

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 10.jpg"
            title="Full board from up front"
            caption="Full board from up front"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 10.jpg" %}

I cut a box I had to get the board to fit and glued the rest of it together. I painted that silver as well.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 12.jpg"
            title="Partial box"
            caption="Partial box"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 12.jpg" %}

Everything fit in place, but was loose. Thankfully, I have lots of hot glue, so I used that.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 16.jpg"
            title="Board in box"
            caption="Board in box"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 16.jpg" %}

I cut another piece of cardboard to make a 'window', glued a piece of clear plastic onto it, and then hot glued that onto the box.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 18.jpg"
            title="Final setup - dark"
            caption="Final setup - dark"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 18.jpg" %}

It's nowhere near close to what it looked like in the movie, but this was more of a rushed job for a party than an actual movie prop replica. (And it's portable!) I used a USB battery pack to power it with no issues.

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 22.jpg"
            title="Final setup - lit up"
            caption="Final setup - lit up"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 22.jpg" %}

If you're interested, take a look at the Teensy [code on github][3].

{% include image.html
            img="images/fluxcapacitor/FluxCapacitor - 5.jpg"
            title="Controls"
            caption="Controls"
            url="https://alvarop.com/images/fluxcapacitor/FluxCapacitor - 5.jpg" %}

The controls on the side consist of two potentiometers and a button all connected to the Teensy. They are used to adjust speed, brightness, and color changes.

<div align="center"><iframe width="640" height="360" src="https://www.youtube.com/embed/k18zvcvC6wI" frameborder="0" allowfullscreen></iframe></div>

[0]: http://www.amazon.com/gp/product/B00VQ0D2TY
[1]: https://www.pjrc.com/teensy/teensyLC.html
[2]: https://hackaday.com/tag/hackaday-superconference/
[3]: https://github.com/alvarop/flux/blob/master/fluxCapacitor/fluxCapacitor.ino

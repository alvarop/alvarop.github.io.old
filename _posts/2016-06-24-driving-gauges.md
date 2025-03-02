---
title: Driving Analog Gauges with DAC
categories:
- projects
tags: []
---

A few years ago, I bought a couple of these analog gauges(galvanometers) at the [electronics flea market][0]. Like many other things I buy, they ended up in a box stored away in the closet… Not too long ago, stumbled onto Alan Wolke's ([@AlanAtTek][1]) [video about panel meters][2]

{% include image.html
            img="images/gauges/IMG_3035.jpg"
            title="Gauge!"
            caption="Gauge!"
            url="https://alvarop.com/images/gauges/IMG_3035.jpg" %}

After watching Alan's video, I decided to pull the gauges out and see if I could make them do something useful. The first thing I looked for after taking them out was the range. The small text on the bottom left says FS=1-0-1 mA DC. I verified this by plugging it into my DC power supply like Alan suggested with a 10kOhm resistor and going from 0-10V. Unfortunately, my power supply doesn't go negative, so I had to reconnect the meter by switching the two wires to test the negative region.

{% include image.html
            img="images/gauges/IMG_3036.jpg"
            title="Behind the gauges"
            caption="Behind the gauges"
            url="https://alvarop.com/images/gauges/IMG_3036.jpg" %}

Ok, so now I have two working gauges that take -1 to 1mA to move. I've been working a lot with the STM32F4-Discovery development board, so I decided to use it, even though it's complete overkill for this project. The microcontroller has two DAC outputs which can be set anywhere from 0-3V. Just add a 3kOhm resistor in series and you can move the needle from 0-10, but how can we get a negative reading?

{% include image.html
            img="images/gauges/IMG_6085.jpg"
            title="FM=1-0-1mA DC"
            caption="FM=1-0-1mA DC"
            url="https://alvarop.com/images/gauges/IMG_6085.jpg" %}

My first thought was to use a tiny H-Bridge circuit that would connect to the DAC output and ground. This would allow the microcontroller to change direction of current flow using two digital outputs. I didn't have any small MOSFETs around, so I tried it with BJTs. It didn't quite work as expected. It also required a bunch of parts and 3 pins per gauge. What a waste! There must be a better way...

{% include image.html
            img="images/gauges/IMG_5551.jpg"
            title="H-Bridge Attempt"
            caption="H-Bridge Attempt"
            url="https://alvarop.com/images/gauges/IMG_5551.jpg" %}

After reading the STM32F407 datasheet for a bit, I found a paragraph that gave me some hope. It basically says you can provide or receive up to 8mA in any GPIO pin. This means that if you connected a resistor between two pins and drove each one high and low, you could have current flowing in both directions, as long as it was less than 8mA. The gauges only need 1mA, so it should be enough.

{% include image.html
            img="images/gauges/datasheet.png"
            title="STM32F407 Datasheet Excerpt"
            caption="STM32F407 Datasheet Excerpt"
            url="https://alvarop.com/images/gauges/datasheet.png" %}

The idea is: If I plug in one end of the gauge(plus resistor) to the DAC and the second to a GPIO, I should be able to get 1mA of current to flow in either direction.

{% include image.html
            img="images/gauges/IMG_3031.jpg"
            title="Connection Example"
            caption="Connection Example"
            url="https://alvarop.com/images/gauges/IMG_3031.jpg" %}

For example, if the DAC is set to 3V and the GPIO is set to 0V, there will be 1mA flowing from the DAC to the GPIO. If we set the DAC to 0V and the GPIO to 3, the 1mA will flow in the other direction. By changing the DAC voltage relative to the GPIO (either 0V or 3V) we can get the full range of -1mA to 1mA.

{% include image.html
            img="images/gauges/IMG_3032.jpg"
            title="Configuration Examples"
            caption="Configuration Examples"
            url="https://alvarop.com/images/gauges/IMG_3032.jpg" %}

Here's a quick video of the gauges moving around with the setup:

<div align="center"><iframe width="640" height="360" src="https://www.youtube.com/embed/xQUWoCiiftM" frameborder="0" allowfullscreen></iframe></div>

So there you have it, an easy, low part count, way of controlling a bidirectional analog gauge with a DAC and a GPIO pin.

[0]: http://www.electronicsfleamarket.com
[1]: https://twitter.com/AlanAtTek
[2]: https://www.youtube.com/watch?v=wbRx5cQZ8Ts

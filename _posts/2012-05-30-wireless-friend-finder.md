---
title: Wireless Friend Finder!
categories:
- cc2500
- projects
tags: []
---
The Wireless Friend Finder was my project for the <a href="https://twitter.com/jeriellsworth/status/202248450362978304">Bring-a-Hack dinner</a> after the 2012 Bay Area <a href="http://makerfaire.com/">Maker Faire</a>. I made it in a hurry, so it's not terribly well documented.

The wireless friend finder is a device that will start buzzing when another device gets near. This can be used to find a friend in a crowd(or to stay away from someone you don't like)! Here's a quick video I did while I was prototyping the project.

<div style="text-align: center;"><iframe src="https://www.youtube.com/embed/2gkRtET5Arc" frameborder="0" width="640" height="360"></iframe></div>

The actual devices consist of an msp430 microcontroller a cc2500 radio, and an annoying buzzer. The devices are sending radio messages every second. If a message from another device is received, the buzzer starts going off. In order to make it slightly more interesting, they measure the signal strength of the incoming message and determine how long the buzzes last. The stronger the signal, the longer the buzz. Here's a video of some outdoor testing. (I had to do it around the apartments to get an ok result. I tried doing it with direct line-of-sight across the parking lot, but after 300ft, it was still buzzing!)

<div style="text-align: center;"><iframe src="https://www.youtube.com/embed/x-Ge8ROIJVA" frameborder="0" width="480" height="360"></iframe></div>

Since the devices aren't very nicely built, I was slightly worried about the airport security. Luckily, they didn't even ask me to take them out of my bags!

{% include image.html
            img="images/wp/IMG_20120517_161712-640x480.jpg"
            title=""
            caption=""
            url="https://alvarop.com/images/wp/IMG_20120517_161712.jpg" %}

Even though the project was for the bring-a-hack dinner, I carried it around while I was at the faire. I was surprised at the reactions it received. Many people were asking if I had plans to make these into an actual product!(And suggesting new features) Moms wanting to find their kids, concert goers wanting to find their friends, burning man attendees, etc... The devices themselves are really cheap, under $10 each, so who knows...

Ian from <a href="http://dangerousprototypes.com/">DangerousPrototypes </a>was nice enough to ask a few questions about the friend finder and put it online (along with other awesome interviews!):

<div style="text-align: center;"><iframe src="https://www.youtube.com/embed/2qkT9hLQPy0" frameborder="0" width="640" height="360"></iframe></div>

So that's the wireless friend finder... If you're interested, you can get the code from <a href="https://github.com/alvarop/msp430-cc2500/blob/master/projects/friendfinder/main.c">github</a>.

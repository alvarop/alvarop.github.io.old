---
title: Automation Progress - Light Alarm and Remote
categories:
- automation
- cc2500
- projects
tags: []
---
If you haven't heard about my 'home automation' project, you should probably <a title="Beginnings of Home(ok, apartment) Automation" href="http://alvarop.com/2013/02/beginnings-of-homeok-apartment-automation/">read this first</a>.

This weekend was rather productive. I managed to get my light alarm working! I wrote <a href="https://github.com/alvarop/pc/tree/master/projects/escheduler">escheduler</a>, which is something like <a href="http://en.wikipedia.org/wiki/Cron">crond</a>, but calls functions, instead of running programs. It's also more limited, since it only schedules events on a weekly basis.

{% include image.html
            img="images/wp/65507_10100403377480335_1815842229_n-640x480.jpg"
            title="Beaglebone with a more 'permanent' radio setup"
            caption="Beaglebone with a more 'permanent' radio setup"
            url="/images/wp/65507_10100403377480335_1815842229_n.jpg" %}

<a href="https://github.com/alvarop/pc/tree/master/projects/escheduler">Escheduler </a>runs on the beaglebone, which is currently my 'home server'. The current set-up turns on the light behind my bed a few minutes before I'm supposed to wake up. Eventually there will be a whole fade-in period, but I just wanted to get something working. I left it running overnight, and sure enough, the lights turned on on time this morning!

Previously, the only way to control the lights was to ssh into the beaglebone and run <a href="https://github.com/alvarop/pc/tree/master/projects/swrite">swrite </a>with the radio commands. You might not think so, but ssh-ing into the server and typing commands from a smartphone in bed at 6am is not as easy as it sounds! To make things easier, I decided to make a web interface I can use from my phone.

{% include image.html
            img="images/wp/BCxhqsqCIAMK9pT-288x480.jpg"
            title="Simple RGB LED controller in smartphone browser"
            caption="Simple RGB LED controller in smartphone browser"
            url="/images/wp/BCxhqsqCIAMK9pT.jpg" %}

It took longer than expected, but I ended up using the <a href="http://twitter.github.com/bootstrap/">twitter bootstrap</a>. I haven't done any web development in several years, so I had to re-learn a lot of things. In the end, I just set up a few buttons to turn the lights on or off. When clicked, there's an AJAX request in the background to a php file that calls <a href="https://github.com/alvarop/pc/tree/master/projects/swrite">swrite </a>to send the commands via the beaglebone radio. Next up will be controlling the actual colors from the web interface, as well as viewing and editing the alarms.

Here's a quick video of the remote in action:

<div align="center"><iframe src="https://www.youtube.com/embed/kFFxp2S3pJk" height="315" width="560" allowfullscreen="" frameborder="0"></iframe></div>

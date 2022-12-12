---
title: CC2500 Project (Part 6) - Reorganizing
categories:
- cc2500
- projects
tags: []
---
This post is mostly about software, so I'll keep it short.

I re-arranged most of the code so it hopefully makes more sense. My goal is to make the main code hardware agnostic. That way if you want to use a different device, you just change which drivers you're using, but your main code stays the same. Eventually I'd like to be able to support multiple devices from multiple manufacturers.

For a much better description, check out the page (and code) on github here: <a href="https://github.com/alvarop/msp430-cc2500" target="_blank">https://github.com/alvarop/msp430-cc2500</a>
(The README file should have some information)

To keep things interesting, here's a quick video on what I was able to do with the current setup. The RGB LED controller(msp430g2452 + cc2500) is wirelessly connected to the PC(msp430g2533 + cc2500 + usb-to-serial converter).

<div style="text-align: center;"><iframe allowfullscreen="" frameborder="0" height="360" src="https://www.youtube.com/embed/H0OEqm4yeYM" width="640"></iframe></div>

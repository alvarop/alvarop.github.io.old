---
title: Using BusBlaster + openOCD on OSX Mavericks
categories:
- ARM
- projects
tags: []
---
I’ve been using the <a href="http://dangerousprototypes.com/">Dangerous Prototypes</a> <a href="http://dangerousprototypes.com/docs/Bus_Blaster">Bus Blaster</a> along with <a href="http://openocd.sourceforge.net/">openOCD</a> to program/debug my LPC1769 microcontroller. It’s been a while since I did anything, so when I tried again last week and couldn’t get it to work, I was slightly confused. The only change (that I was aware of) was an OSX upgrade from Mountain Lion to Mavericks.

Whenever I tried to run openOCD, I would get the following error:
<strong>Error: unable to open ftdi device: unable to claim usb device. Make sure the default FTDI driver is not in use</strong>

I tried reinstalling the FTDI drivers (both <a href="http://www.ftdichip.com/Drivers/VCP.htm">VCM</a> and <a href="http://www.ftdichip.com/Drivers/D2XX.htm">D2XX</a>), unloading them, reloading, and several other things without any luck. Whenever I plugged the BusBlaster in, two devices would show up under <strong>/dev</strong>. <strong>/dev/cu.usbserial-1d11A</strong> and<strong> /dev/cu.usbserial-1d11B</strong>. This meant that the FTDI driver was working, but at the same time, stopping openOCD from using the device. What did not make sense was that this was happening even when I unloaded the FTDI kext.

After some research, I found out that since OSX Mavericks, the <a href="https://developer.apple.com/library/mac/technotes/tn2315/_index.html">AppleUSBFTDI</a> kernel driver is included by default. This was the one setting up the usbserial devices whenever I plugged the device in. The main solution everyone seemed to have was to unload <strong>AppleUSBFTDI</strong> using:
<strong>sudo kextunload -bundle com.apple.driver.AppleUSBFTDI </strong>

Finally! After unloading the kext, openOCD started working again. Unfortunately, this means that you can’t use any usb-serial devices anymore, because the kext isn’t loaded… That’s unfortunate.

Luckily, I had an idea. What if I unload the kext, run openOCD, then load it again? It worked! OpenOCD was still working and the rest of the FTDI usb-serial devices were loaded. Finally a working solution that didn’t cripple the system. This still requires me to unload/load the kext every time I want to use openOCD, which is not a terribly elegant solution.

During my research into the problem, I ran into a<a href="https://forum.sparkfun.com/viewtopic.php?t=8923"> forum post </a>with a similar problem, except it was in 2007 and instead of the Apple FTDI driver, it was the regular FTDI driver causing problems. Their solution had them edit the kext's<strong> Info.plist</strong> to make sure the driver didn’t do anything to a particular usb device. (Using product and vendor id’s) That got me thinking that maybe I could do the same with the Apple kext.
To do this, open: 

{% highlight bash %}
/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBFTDI.kext/Contents/Info.plist
{% endhighlight %}

Find the device you want excluded, in this case <strong>AppleUSBEFTDI-6010-0</strong> and comment out the key and dictionary. (I looked up the product id on OSX's System Information window)

{% include image.html
            img="images/wp/Screen-Shot-2014-01-05-at-8.05.07-AM-640x362.png"
            title="FTDI Device Id"
            caption="FTDI Device Id"
            url="https://alvarop.com/images/wp/Screen-Shot-2014-01-05-at-8.05.07-AM-640x362.png" %}

Now you just have to reload the kext and everything should work without having to load/unload kexts every time!
<strong>sudo kextunload -bundle com.apple.driver.AppleUSBFTDI</strong>
<strong>sudo kextload -bundle com.apple.driver.AppleUSBFTDI</strong>

{% include image.html
            img="images/wp/Screen-Shot-2014-01-05-at-8.03.31-AM-432x480.png"
            title="AppleUSBFTDI.kext Info.Plist"
            caption="AppleUSBFTDI.kext Info.Plist"
            url="https://alvarop.com/images/wp/Screen-Shot-2014-01-05-at-8.03.31-AM.png" %}

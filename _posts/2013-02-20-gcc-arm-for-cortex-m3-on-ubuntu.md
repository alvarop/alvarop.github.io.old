---
title: GCC-ARM for Cortex-M3 on Ubuntu
categories:
- ARM
- projects
tags: []
---
Don't want to read though this post? Just want the code, go get it from my <a href="https://github.com/alvarop/arm-gcc-barebones">github repo</a>!

I've been meaning to start working with Cortex-M3 processors for a few of my projects. Sometimes the MSP430's I usually use just aren't fast enough. :-)

Previously, I've used the <a href="http://mbed.org/">mbed</a>, which is a nice Cortex-M3(LPC1768) development board. The best part about it is that you program it by just copying the bin file to it as if it was a flash drive. It takes care of the actual device programming for you. The downside is that you don't have any debugging capabilities, and that you have to use their online compiler.

The online compiler isn't so bad, but you have to use their libraries and it's all in C++. When working with microcontrollers, I prefer plain old C. To get around this, I decided to figure out how to use the <a href="https://launchpad.net/gcc-arm-embedded">GNU GCC-ARM compiler</a> so I could have full control of the processor. I'm not going to cover every step I took, because that's boring, but here's a quick summary of how it went. (You can also look at my <a href="https://github.com/alvarop/arm-gcc-barebones/commits/master">commit history</a> for more details).

While trying to figure out what flags to pass to the compiler to build the most basic program, I found out the online mbed compiler has a 'recently' added <a href="http://mbed.org/handbook/Exporting-to-GCC-ARM-Embedded">export feature</a>! You write your program with their online, C++, compiler, export it for gcc-arm, then you can build it all off-line. They include all the pre-compiled libraries and header files required, along with a nice Makefile. This made my life much easier. Now all I had to do was start cutting stuff out until I was happy.

I started by switching the main file to C, from C++. I then started removing all of their included libraries. Eventually, I was able to remove all of their files and start using the standard <a href="http://ics.nxp.com/support/lpcxpresso/">CMSIS headers</a>. I had to find a plain C version of the startup\_LPC17xx.c from some other <a href="http://www.nxp.com/products/microcontrollers/cortex_m3/LPC1768FBD100.html#documentation">code! examples</a> on NXP's site. Finally, I had a very basic Makefile that built an LED blinky program that actually worked on the mbed.

One thing that was slightly disturbing was that my blinky program was ~20kB! That is way too big! Turns out they were including things like the C math library and floating-point versions of scanf and printf! I don't need that... Now the code is ~2.5kB, which is still a bit high, but not 20kB!

So that was my experience getting started with the gcc-arm compiler. You can get the code from my <a href="https://github.com/alvarop/arm-gcc-barebones">github repo</a>. I will keep updating this as I learn more. My goal is for every new ARM project I work on to start from here.

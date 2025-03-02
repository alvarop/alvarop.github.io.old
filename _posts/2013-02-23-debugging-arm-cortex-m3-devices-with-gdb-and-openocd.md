---
title: Debugging ARM Cortex-M3 Devices with GDB and openOCD
categories:
- ARM
- projects
tags:
- arm
- cortex-m3
- gcc
- gdb
- lpc1769
---

After <a title="GCC-ARM for Cortex-M3 on Ubuntu" href="http://alvarop.com/2013/02/gcc-arm-for-cortex-m3-on-ubuntu/">getting the gcc-arm compiler working with the mbed</a>, I decided to take a look at my <a href="http://www.lpctools.com/lpc1768.lpcxpresso.aspx">LPCXpresso LPC1769</a> development board. The mbed is really easy to program. It mounts as a flash drive and you just drag and drop the binary file onto it. Unfortunately, that's it. There is no way to get any debug information out of it. The LPCXpresso, on the other hand, comes with a nice LPC-link board attached just for this purpose. Unfortunately(again), it only works with certain IDE's, like <a href="http://www.code-red-tech.com/">code\_red</a>. I cut the lpc-link board off and instead used a <a href="http://dangerousprototypes.com/docs/Bus_Blaster">BusBlaster </a>from Dangerous Prototypes along with <a href="http://openocd.sourceforge.net/">OpenOCD</a>. It took me a while to actually program the device, so I'll leave that for later. This post is about debugging!

{% include image.html
            img="images/wp/IMG_0037.jpg"
            title="BusBlaster and LPCXpresso LPC1769"
            caption="BusBlaster and LPCXpresso LPC1769"
            url="https://alvarop.com/images/wp/IMG_0037.jpg" %}

So why, you might ask, do I go to all this trouble to get a debugger working? Because debuggers are awesome! Without them, one has to resort to printf statements(if you're lucky enough to have that working) and LED's. Sure, those are useful sometimes, but having access to memory, registers, stepping through code, etc. makes debugging much easier!

* <strong>All of the following takes place in Ubuntu 12.04.</strong>
* <strong>I'm using a simple<a href="https://github.com/alvarop/arm-gcc-barebones/blob/master/main.c"> blinking led program </a>as an example</strong>
* <strong>Here's some <a href="http://dangerousprototypes.com/docs/Bus_Blaster_OpenOCD_guide">info about openOCD and the BusBlaster</a></strong>


1. <a href="http://alvarop.com/2013/02/gcc-arm-for-cortex-m3-on-ubuntu/">Compile </a>your code with arm-gcc and make sure to pass the -g flag to generate debugging information.

2. Run openOCD to connect to the device.

    `$ openocd -f openocd.cfg`

3. Run GDB and connect to openOCD

    `$ arm-none-eabi-gdbtui -ex "target remote localhost:3333" blink.elf`

    If you see [No source available], it's probably because the core is running. Do the following to halt it the first time:

    `(gdb) continue`

    `(gdb) Ctrl+c`

    The c source should now be visible

4. Setup split view to see dissasembly (if you want)

    `(gdb) layout split`

5. Debug away!

{% include image.html
            img="images/wp/split.png"
            title="Split view in GDB"
            caption="Split view in GDB"
            url="https://alvarop.com/images/wp/split.png" %}

It's been a while since I use GDB, but here are some examples of commands that are useful:

* <strong>(gdb) Ctrl+C</strong> - Halts execution
* <strong>(gdb) step/next</strong> - step through a line (of c code)
* <strong>(gdb) stepi/nexti</strong> - step through an individual instruction
* <strong>(gdb) continue</strong> - Continue execution
* <strong>(gdb) break 22</strong> - set a breakpoint in line 22 (you can also name a function instead)
* <strong>(gdb) delete</strong> - get rid of all the breakpoints
* <strong>(gdb) where/backtrace</strong> - print backtrace of all stack frames
* <strong>(gdb) info locals</strong> - see local variables
* <strong>(gdb) info registers</strong> - see all registers and values
* <strong>(gdb) x/2xw 0x2009C018</strong> - show 2 words(in hex!) starting from memory address 0x2009C018
* <strong>(gdb) set {uint32_t}0x2009C018 = 0x400000</strong> - set value of memory address 0x2009C018 to 0x400000

There are many more things you can do with GDB. For more info. check out <a href=" http://www.delorie.com/gnu/docs/gdb/gdb_toc.html">Debugging with GDB</a>.


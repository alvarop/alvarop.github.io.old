---
title: Projects Update
categories:
- projects
tags: []
---
I’ve decided to actually write about what I’ve been up to in the past few years. Today, I’m going to start with a project from the summer of 2006. I decided to go to <a href="http://www.defcon.org/">DEFCON</a> and take part in the <a href="http://defconbots.org/">defconbots </a>competition. The main goal of the competition was to build a device that shot targets using autonomous control only. You can see the competition page <a href="http://defconbots.org/defcon14/">here</a> and the <a href="http://defconbots.org/defcon14/final_results.php">results</a>. Unfortunately, I didn’t start working on it until two or three weeks before.
Here’s a brief description of how it happened. Since I was right out of high school, my budget was extremely limited. I decided to get a webcam mount with two servos and a USB servo controller, along with a really cheap BB gun.

{% include image.html
            img="images/blgr/1.jpg"
            title="One of three BB guns"
            caption="One of three BB guns"
            url="https://alvarop.com/images/blgr/1.jpg" %}

{% include image.html
            img="images/blgr/6.jpg"
            title="USB Servo Controller"
            caption="USB Servo Controller"
            url="https://alvarop.com/images/blgr/6.jpg" %}

After receiving the gun, I took it apart to figure out how it worked. It was basically a DC motor with some gears pulling back a spring that loaded, then fired, the BBs

{% include image.html
            img="images/blgr/2.jpg"
            title="Firing Mechanism"
            caption="Firing Mechanism"
            url="https://alvarop.com/images/blgr/2.jpg" %}

{% include image.html
            img="images/blgr/3.jpg"
            title="The Guts"
            caption="The Guts"
            url="https://alvarop.com/images/blgr/3.jpg" %}

Instead of buying a webcam, I took one from my dad and (after some modifications) mounted it in front of the gun.

{% include image.html
            img="images/blgr/5.jpg"
            title="Cannibalized Webcam"
            caption="Cannibalized Webcam"
            url="https://alvarop.com/images/blgr/5.jpg" %}

{% include image.html
            img="images/blgr/8.jpg"
            title="Gun with Mount and Webcam"
            caption="Gun with Mount and Webcam"
            url="https://alvarop.com/images/blgr/8.jpg" %}

At the time, my knowledge of programming was limited to PHP and VisualBasic. I figured out how to talk to the webcam and servo controller using VB and proceeded to write my aiming program. I had no idea about any image processing algorithms or anything like that, so I had to make it very simple. The targets were lit by infrared LED’s, and by using a filter in front of the webcam, I was able to isolate IR light from everything else. My high tech filter consisted of some developed film. After going through the filter, infrared light showed up as white pixels, while everything else was red or black. This allowed me to “find” IR light by counting white pixels in the image. I divided the image into a grid and counted how many white pixels were in each section. After figuring out which square had the most white pixels, I would move the gun in that direction. Once the most white pixels were in the center of the image, the gun would fire until the lights disappeared.

{% include image.html
            img="images/blgr/7.jpg"
            title="Fancy IR Filter and Laptop with Aiming Program"
            caption="Fancy IR Filter and Laptop with Aiming Program"
            url="https://alvarop.com/images/blgr/7.jpg" %}

I tried a few different methods for firing the gun, but ended up going with the simplest. I connected another servo and glued a temporary switch to it. All I needed to do to fire was move that servo so it would push the button and close the circuit driving the DC motor in the gun.

{% include image.html
            img="images/blgr/4.jpg"
            title="Firing Servo"
            caption="Firing Servo"
            url="https://alvarop.com/images/blgr/4.jpg" %}

The gun was not designed to hold too many BBs, so I added a parmesan cheese container to hold more. After everything (almost) worked, I packed it in a box and flew to Vegas. The TSA people were rather intrigued when they searched my luggage, but let me through after a few minutes.
The actual competition was a lot of fun. I came in 5th place (out of 6), but had a lot of fun doing it. Some of the competition consisted of university senior design projects with awesome equipment, so I really had no chance. Here are some photos from the competition. These last two photos were not taken by me. I can’t find who took the second one, so if it’s you, let me know so I can give appropriate credit!

{% include image.html
            img="images/blgr/IMG_5719.jpg"
            title="During Competition"
            caption="During Competition"
            url="https://alvarop.com/images/blgr/IMG_5719.jpg" %}

Oh, I also added an “about me” page over <a href="/about">here</a>.

---
layout: post
title: "Introducing: LeadMe"
date: 2014-12-23 12:00
author: dimitar
tags: [circuits, product, android]
---

  *This is a collaborative post by <a href="http://dimitar.io" target="_blank">Dimitar</a> and <a href="http://dakotanelson.com" target="_blank">Dakota</a>.*

  We made a cool thing this semester - a small vibrating silicon anklet that helps you get around.  Warning: shameless plug ahead - we’re very excited about it!

{:.center}
![ankle]({{site.url}}/assets/leadme-ankle.jpg){: .image }

  For many, navigation can be difficult. Even though we rely on accurate GPS nearly every day, the way we use it basically hasn’t changed since humans invented maps - staring at a drawing of the world and following a line on it, connecting where you are to where you want to go. Although smartphones make finding a route easy, following it is still a pain. Checking your map while walking is annoying, and it only gets worse if you’re out on a run.  If you’re biking, it can be fatal. And for many with vision impairments, looking at a map isn’t even an option.

  LeadMe seeks to alleviate this daily difficulty. With five carefully calibrated vibrating motors inside a sleek silicone anklet, LeadMe guides you to your destination without forcing you to stare at your phone. Simply put the anklet on, choose your destination in our Android app, then follow the vibrations to where you’re going, all without hands, eyes, and, after a little bit of practice, even conscious attention.  (Trust us!)

  LeadMe consists of five coin-type vibrating motors encased in silicone, controlled over Bluetooth by an Android phone, all powered by a LiPo battery. The electronics are split into 5 basic boards:

  * A power board consisting of a 3v3 MIC5205 linear regulator (which is great because it has decent accuracy and very low ground current) and a MCP73831 USB LiPo charger wired to a MicroUSB receptacle at the rear of the device. This charges and discharges a single-cell 240 mAh LiPo battery.

  * A control board built around a TQFP ATMega328 (AU) with an external 16MHz crystal.  The firmware on the board utilizes the Arduino bootloader and a custom script. The script receives direction instructions over UART (coded with a custom protocol optimized for the anklet) and determines PWM outputs for some of five different ports, mixing duty cycles to estimate the direction as precisely as possible. It also returns current PWM values.  We are debating adding an FTDI converter connected to the charging USB port for firmware updates.

  * A motor driver board (basically a set of N-MOSFETs) drives the five vibrating motors, using the PWM signals from the control board to vary the intensity of vibration. This enables LeadMe to blend two motors together, providing more nuanced directions than just turning the five motors on and off.

  * A Bluetooth board (the only board not custom-made, built around the HC-05, a wildly popular BC417-based module) communicates with the controlling device, for now limited to an Android phone. LeadMe uses your phone’s location data, keeping the anklet simple, small, and low-power.  The access PIN for the device can be changed from the default once the user is connected.

  * A minimal power button circuit between the LiPo and the power board, which uses a P- and N-MOSFET to form an SR latch.  The R line has a 10uF cap inline that requires holding the button for a few seconds to turn everything off, preventing accidental presses.  One of the FETs has the double function of actually switching on power.  The button also sends a signal to the micro if it is pressed (and not held) which can be used for features not yet determined.  When off, this is the only circuit that draws current - on the order of micro-amps.

  Here are pictures of some home-brewed PCB prototypes:

{:.center}
![power]({{site.url}}/assets/leadme-power.jpg){: .flow-image}
![control]({{site.url}}/assets/leadme-control.jpg){: .flow-image}
![motor]({{site.url}}/assets/leadme-motor.jpg){: .flow-image}

<!-- hacky, but it works -->
<br style="clear:both;" />

If you’re interested in more details on LeadMe’s design and construction, head over to our website, [http://burgers-n-fries.github.io](http://burgers-n-fries.github.io).

  This project began in an engineering class at our school, Olin College (we’re all students there). In addition to Dakota and Dimitar, your authors, the team is composed of Nagy Hakim, Chris Wallace, and Philip Seger. Hopefully, you’ve read some of Dakota’s posts already.  He is the backbone of the team, and LeadMe is his brainchild.  Dimitar is the EE who made the electronics inside - all surface mount, on custom fabbed boards - possible.  He promises he’ll start posting more in the future. Nagy is the brilliant mechanical engineer who made this sturdy, comfortable and, dammit, sexy casing.  Chris is the developer behind our beautiful, robust Android application.  Last but not least, Phillip is our UI expert, responsible for our website, [http://burgers-n-fries.github.io](http://burgers-n-fries.github.io).

{:.center}
![render]({{site.url}}/assets/leadme-render.jpg){: .image }

  We’re continuing work on LeadMe at the very least throughout this next semester, with plans to release it to the public soon - likely through Kickstarter. If you’re interested, keep an eye on this blog as we move forward.  If you’re really excited, drop us a line - we’d be happy to chat! LeadMe is still in heavy development, and we’re very open to ideas along the way.

  Thanks and see you soon!

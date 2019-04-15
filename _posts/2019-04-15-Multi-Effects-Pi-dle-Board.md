---
layout: post
title: Multi-Effects Pi-dle Board
---


### Guitarix- The Pi-dle Board

Blog Post about Guitarix raspberry pi multi-effects board build

**Note: **This is an intermediate to advanced project. Not recommended for
beginners to Raspberry Pi/ DIY electronics projects. Proceed at your own risk. I
am not responsible for your actions during this process. This is a *very*
lengthy process.**

### The Dream

![](https://cdn-images-1.medium.com/max/600/0*eT9Owa0s3VQgag2I.jpg)
<span class="figcaption_hack">DIY Effects Pedal from [kalebaiton](https://imgur.com/user/kalebaiton)</span>

Ever since I first discovered the Raspberry Pi microcomputer, I’ve been
fascinated with tinkering with them for projects. For a $35 microcomputer, they
are surprisingly robust and powerful and are capable of many different tasks and
uses as I’ve mentioned in (LINK) previous posts. Needless to say, I’ve always
wanted to try to build a budget-friendly DIY guitar effects/ amp simulator
pedalboard. Similar to other pedalboards on the market, the pedal board would be
able to switch between a number of custom programmed effects and tones.
Additionally, options such as a volume or expression pedal, and status lights/
displays for each “pedal” could be implemented as time goes on as well. There
are many other options on the market such as Boss pedalboards, Kemper amps, or
the high-cost Axe-FX system. As with most audio gear, these can drive a high
price, making them hard to access. So having just finished my Pi-Hole project
and OBVIOUSLY needing another one, I began researching solutions on the
raspberry pi platform.

<br> 

### Options Options Options

1.  Pedal-Pi
1.  Pure Data
1.  Csound
1.  Guitarix

![](https://cdn-images-1.medium.com/max/600/0*F-KyTQ6UtbE3K7w5.jpg)

Initially, I discovered the [Pedal-Pi](https://www.electrosmash.com/pedal-pi), a
Raspberry Pi Zero-based single guitar pedal capable of custom pedal effect
programming. I might want to follow up with this later, but for my application,
I’m looking for more than one programmable effect/pedal. After researching a bit
further, it seemed like my main two choices for effects programs would be [Pure
Data](https://puredata.info/); “a visual programming language developed by
Miller Puckette in the 1990s for creating interactive computer music”, or
CSound; “ a computer programming language for sound [designed to] synthesize,
and manipulate digital audio”. To be honest, I was more than a little
intimidated by the lack of options. Both Pure Data and CSound seem to have small
niche communities surrounding them, but the software and application were
archaic and not very user-friendly. 

![](https://cdn-images-1.medium.com/max/600/0*iY2g92KruNrkSDSe.jpg)

Fortunately, before getting too far down the Pure Data/CSound rabbit hole I
discovered *Guitarix*. Guitarix is “a virtual guitar amplifier for Linux running
on [Jack Audio Connection Kit](http://jackaudio.org/).” Guitarix offers a
digital rack that is fully customizable and programmable. It even offers
simulations of classic pedals, amplifiers, tones, as well as compressors and EQ.
In short, you can create and customize your very own unique sound and save it as
a preset for later use.

<br> 

### Latency- The Beast of Burden

![](https://cdn-images-1.medium.com/max/600/0*oqCwkE4g7961_fU3.jpg)

The largest concern I had when initially researching this project was the CPU
power and latency limitations of a Raspberry Pi 3b and a USB DAC (Digital to
Analogue Converter). Many other projects appear to have used audio interfaces
but this would not fit our small pedalboard size restrictions or budget.
Luckily, through overclocking and a proper power supply, I was able to get the
latency down to about 5ms without too much restriction, which is more than quick
enough.

<br> 

### Tutorial

<br> 

![](https://cdn-images-1.medium.com/max/600/0*ya9zlUJ_9_F84cNm)

Note: This is an intermediate to advanced project. Not recommended for beginners
to Raspberry Pi/ DIY electronics projects. Proceed at your own risk. I am not
responsible for your actions during this process. This is a **very** lengthy
process.

<br> 

### Bill of Materials

<br> 

### Phase 1- Set up Raspberry Pi

![](https://cdn-images-1.medium.com/max/600/1*J0xtvElCr4c4BGHUuPROyg.png)

1.  Download [Raspberrian Stretch
](https://www.raspberrypi.org/downloads/raspbian/)(Desktop) 
1.  Extract image from zip file
1.  Burn Image to SD card via [Win32 Disk
(Windows)](https://sourceforge.net/projects/win32diskimager/) or [Balena Etcher
(MAC)](https://www.balena.io/etcher/)

4. Plug in SD card / peripheral connections to Raspberry Pi and boot up

![](https://cdn-images-1.medium.com/max/800/0*ZuD24plkqpAkqsRA.gif)

5. Connect to local wifi and enable VNC connections with `sudo raspi-config` in
terminal.

![](https://cdn-images-1.medium.com/max/800/0*uroG8naXy01Cl-7B.png)

6. Navigate to Interfacing Options and enable VNC connections.

7. Reboot and connect through VNC on desktop/laptop 

8. Lastly, change the [GPU/ CPU
settings](https://howtoraspberrypi.com/how-to-overclock-raspberry-pi/) to
“Overclock” the pi, which will provide maximum performance. (Note: you will
**need** the proper power supply and heat sinks/fans for this step) You may need
to tinker with the numbers specifically for your pi. Some can handle 1350
arm_freq, and some can only handle 1000.

![](https://cdn-images-1.medium.com/max/800/1*RxpxE6WzVz3zP6sm6Sw-DQ.png)

NOTE: Steps 5 and 6 are not required but I found that it was easier to remotely
configure the Pi (especially since we will eventually be setting it up in
‘headless mode’)

### Phase 2 — Guitarix & JACK

Now that you have a Stretch setup in desktop mode we can install Guitarix and
Jack. JACK handles the audio input and output connections from the Pi, while
guitarix adds the desired effects.

![](https://cdn-images-1.medium.com/max/600/0*ByjbtSmEGCALyShP)

1.  Connect USB DAC and input/output cables
1.  Select USB DAC as primary audio device in sound settings
1.  Go to Preferences →Add/ Remove Software → guitarix 

This should download guitarix as well as the Jack Audio Connection Kit (JACK)

4. Start guitarix (run desktop icon)

![](https://cdn-images-1.medium.com/max/600/0*D5YS_aG_Bpa_TO1q.png)

5. This should load up a message that prompts starting JACK Server (since it is
not currently running) Click YES

6. You should see something like ←this

7. In JACK application window, click “Connect” button and drag connections to
reflect below. Capture 1 is your audio in, and playback 1/2 is your audio
output.

![](https://cdn-images-1.medium.com/max/800/0*lVzm2WZv1tJQtPlp.png)

8. Navigate to the “Setup…” tab in JACK and match these settings. If these
settings are not properly configured, there will be notable latency.

![](https://cdn-images-1.medium.com/max/800/0*65E2w8ntQpbRE7W7.png)

![]()

9. Edit Guitarix settings (NEED MORE INFO)

10. You should be able to play through guitarix now

![](https://cdn-images-1.medium.com/max/800/0*GxilY90qNEVwYmJu.jpg)

For more information about [guitarix ](http://guitarix.org/)see the
[wiki](https://sourceforge.net/p/guitarix/wiki/Main_Page/).

11. Once everything is configured and operating to your liking, I would
**strongly advise** creating an image backup through a program like [apple pi
baker.](https://www.tweaking4all.com/software/macosx-software/macosx-apple-pi-baker/)

### Phase 3 — Guitarix/ JACK Autostart On Boot

<br> 

<br> 

### Phase 4 — Switching Presets

<br> 

<br> 

### Phase 5 — Building the Enclosure

<br> 

<br> 

<br> 





| Output | X |   |  Y |
|:------:|:-:|:-:|:--:|
|    1   | 7 | + |  9 |
|    2   | 7 | + |  8 |
|    3   | 7 | + |  1 |
|    4   |   | + |    |
|    5   | 5 | + | 10 |
|    6   | 5 | + | 13 |
|    7   | 6 | + | 14 |
|    8   | 7 | + |  4 |
|    9   | 6 | + | 13 |
|   10   | 3 | + | 14 |



---
layout: post
title: Multi-Effects Pi-dle Board
---
![](https://github.com/AnthonyTippy/Images/blob/master/Pedal%20Board%20Banner.png?raw=true)

### Guitarix- The Pi-dle Board

**Note:** *This is an advanced DIY project. Not recommended for beginners to
Raspberry Pi/ DIY electronics projects. Proceed at your own risk. I am not
responsible for your actions during this process. This is a very lengthy
process. Previous experience with Linux terminal and soldering is recommended*

### The Dream

<br> 

![](https://cdn-images-1.medium.com/max/800/1*cwAtrj5FN9QI3uKJTr--6A.jpeg)

Ever since I first discovered the Raspberry Pi microcomputer, I’ve been
fascinated with tinkering with them for projects. For a $35 microcomputer, they
are surprisingly robust and powerful and are capable of many different tasks and
uses as I’ve mentioned in previous posts. Needless to say, I’ve always
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
processing power and latency limitations of a Raspberry Pi 3b and a USB DAC
(Digital to Analogue Converter). Many other projects appear to have used audio
interfaces but this would not fit our small pedalboard size restrictions or
budget. Luckily, through overclocking and a proper power supply, I was able to
get the latency down to about 5ms without too much restriction, which is
sufficient.

<br> 

### Tutorial (A General How-To)

<br> 

![](https://cdn-images-1.medium.com/max/600/0*ya9zlUJ_9_F84cNm)

Note: This is an intermediate to advanced project. Not recommended for beginners
to Raspberry Pi/ DIY electronics projects. Proceed at your own risk. I am not
responsible for your actions during this process. This is a **very** lengthy
process.

<br> 

### Bill of Materials

Here is also a [Google Drive
Link](https://docs.google.com/spreadsheets/d/1G8jwDxUFVlETbdXkdR91Q11LxfasgQAYwSIBFPBOx10/edit?usp=sharing)
with Amazon links attached. The bare minimum cost will is $105 without the
enclosure. I tried to keep the pedal as affordable as possible in the spirit of
the build, however, you could build this for anywhere from $105–300 depending on
your customization options (touch screen, volume pots, power brick, nicer
woods…etc)

![](https://cdn-images-1.medium.com/max/800/1*0n997b9IwZpcPoOvsF8eGA.png)

---

### Phase 1- Set up Raspberry Pi

![](https://cdn-images-1.medium.com/max/600/1*J0xtvElCr4c4BGHUuPROyg.png)

1.  Download [Raspberrian Stretch
](https://www.raspberrypi.org/downloads/raspbian/)(Desktop) 
1.  Extract image from zip file
1.  Burn Image to SD card via [Win32 Disk
(Windows)](https://sourceforge.net/projects/win32diskimager/) or [Balena Etcher
(MAC)](https://www.balena.io/etcher/)

1. Plug in SD card / peripheral connections to Raspberry Pi and boot up

![](https://cdn-images-1.medium.com/max/800/0*ZuD24plkqpAkqsRA.gif)

1. Connect to local wifi and enable VNC connections with `sudo raspi-config` in
terminal.

![](https://cdn-images-1.medium.com/max/800/0*uroG8naXy01Cl-7B.png)

1. Navigate to Interfacing Options and enable VNC connections.

1. Reboot and connect through VNC on desktop/laptop 

1. Lastly, change the [GPU/ CPU
settings](https://howtoraspberrypi.com/how-to-overclock-raspberry-pi/) to
“Overclock” the pi, which will provide maximum performance. (Note: you will
**need** the proper power supply and heat sinks/fans for this step) You may need
to tinker with the numbers specifically for your pi. Some can handle 1350
arm_freq, and some can only handle 1000.

![](https://cdn-images-1.medium.com/max/800/1*RxpxE6WzVz3zP6sm6Sw-DQ.png)

NOTE: Steps 5 and 6 are not required but I found that it was easier to remotely
configure the Pi (especially since we will eventually be setting it up in
‘headless mode’)

---

### Phase 2 — Guitarix & JACK

Now that you have a Stretch setup in desktop mode we can install Guitarix and
Jack. JACK handles the audio input and output connections from the Pi, while
guitarix adds the desired effects.

![](https://cdn-images-1.medium.com/max/600/0*ByjbtSmEGCALyShP)

1.  Connect USB DAC and input/output cables
1.  Select USB DAC as a primary audio device in sound settings
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

---

### Phase 3 — Guitarix/ JACK Autostart On Boot

Now that, we have Guitarix installed on Raspberrian, we need to make our
raspberry pi automatically start and run both Jackd for audio, and Guitarix for
effects processing upon boot initialization. We can do this with the following
steps: (LINK
[https://raspberrypi.stackexchange.com/questions/8734/execute-script-on-start-up](https://raspberrypi.stackexchange.com/questions/8734/execute-script-on-start-up))

1.  Create a Startup Script (Copy this script for step 2)
    ~~~~
    pkill jackd
    pkill guitarix 

    /usr/bin/jackd -dalsa -dhw:Device -r192000 -p512 -n2
    
    guitarix
    ~~~~
    Note:  I ended up having to create 2 start-up scripts due to complications.  Your mileage may vary
    

2. Create a file for your startup script and write your script in the file:


3. Copy and paste in your script from Step 1.

4. Save and exit: Ctrl+X, Y, Enter

5. Make the script executable:


5. Register script to be run at startup:


7. Auto-login

Next, we will need to ensure that the pi does not get stuck at a login screen
during initialization. The simplest way to do so is — 


![](https://cdn-images-1.medium.com/max/800/0*rh9dsmKytfz3PBjU.png)

7. Finally, reboot your pi 

Your pi should boot up, log in, and start Jack and guitarix automatically. You
will be able to hear fuzz or your instrument (if plugged in) at this point.

---

### Phase 4 — Preset Switching

There a number of ways we could facilitate the switching of presets and other
functions within Guitarix such as using the GPIO (General Input and Output)
pins, or homebrewing our own MIDI control, however, due to the inherent
difficulty of this project I’ve opted for the simplest option- External Keyboard
Encoder.

Luckily for us, Guitarix offers a number of very useful keyboard shortcuts; the
most basic being for switching presets with numbers 1–10. So if we can route our
momentary footswitches to keyboard numbers 1 -10, then we will have 10
functional switches to navigate between presets.

**Ok, how do we do that though…**

To accomplish this, we will solder directly to the header pins of a wired
keyboard, then connect each footswitch to the appropriate header combinations to
result in the correct value.

Unfortunately, each keyboard is different, and though there are some [helpful
guides](https://www.xsimulator.net/community/faq/button-box-made-from-a-keyboard.231/),
we will have to find the correct X, Y header combinations ourselves. What does
that mean?

![](https://cdn-images-1.medium.com/max/800/1*f_3pbT5I-cRoFCYR3oQYxg.jpeg)

**Time to break out our test leads!**

![](https://cdn-images-1.medium.com/max/800/0*Hs-qIICicjz3lqLO.jpg)

![](https://cdn-images-1.medium.com/max/800/1*kn7Bl5vLBj5e5z_RA2HQ3w.jpeg)

To discover the correct combination of X and Y headers, it is recommended to use
a single cable with a test probe as shown above on each end. Plug your keyboard
into your computer. Carefully, connect one end to one header pin (X), to another
(Y), and see what is typed when you do this. This will take a decent amount of
tinkering to find the right combinations to output the values you want.

Here are the combinations for my keyboard — 

![](https://cdn-images-1.medium.com/max/800/1*F5RBBOHp1ICuSGxkqtIq3Q.png)

Now that we know the combinations, we simply need to connect each footswitch to
the proper headers. For example, per the table above, footswitch 1 would connect
to 7 (X) and 9 (Y). Here is a rough diagram I’ve drawn up of the connections.

![](https://cdn-images-1.medium.com/max/1200/1*W5X-r93VBin2MOKhqTBVOw.png)

Here is my *very messy* version of this for my prototype.

![](https://cdn-images-1.medium.com/max/800/1*0mqvX24CnPA08UC5xi4mvw.jpeg)

**At last, A prototype!**

![](https://cdn-images-1.medium.com/max/800/1*CYA6OaUwA3yqOkCZPt27-w.jpeg)

![](https://cdn-images-1.medium.com/max/800/1*CW_0UsQZCzq3btqkI8humw.jpeg)

---

### Phase 5 — Building the Enclosure

*CURRENTLY IN PROGRESS*

I’ve based the enclosure design around a pedal board design from [Merwin
Music](https://www.youtube.com/watch?v=KUfju5pGoXo). 

![](https://cdn-images-1.medium.com/max/800/1*igY9o9UmwgdG_OKs4RFDTw.jpeg)

![](https://cdn-images-1.medium.com/max/800/1*4aUUBJ2Em7JnORn9FxjI2w.jpeg)

---

### Phase 6— Finalization

IN PROGRESS



### New to effects pedals or wanna learn more? 
Check out [Beginner Guitar HQ](https://beginnerguitarhq.com/bass-effect-pedals/) for a great introduction to the various effects pedals and their functions.

<br> 

<br> 

<br> 



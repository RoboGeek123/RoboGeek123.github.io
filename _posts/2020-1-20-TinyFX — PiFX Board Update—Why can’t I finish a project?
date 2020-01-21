---
layout: post
title: TinyFX — PiFX Board Update—Why can’t I finish a project?
---


![](https://cdn-images-1.medium.com/max/1628/1*Wr1Dv2NEqYZfCXCIZMkLwg.png)

Many of you will recall my post about the [PiFX Guitarix Multi-Effects Board](https://medium.com/@atippy83/guitarix-the-pi-dle-board-8d6298ca8e42?source=your_stories_page---------------------------) I was building last year. Firstly I’d like to say a huge _THANK YOU!_ to everyone who read my blog post about the project. I was even featured on [Hackaday](https://hackaday.com/2019/05/27/pifx-the-pi-powered-pedal-board/) at one point, something that still blows my mind today. Thank you for your support!

Anyways, I _am_ still working on the PiFX Multi-Effects board, however, I’ve taken a bit of a break from the project since the Raspberry Pi 3b+ I was using at the time shorted out. RIP. So until I get another Pi, the project is temporarily on hold. In the meantime, I’ve been utilizing my [Monoprice Select Mini V2](https://www.monoprice.com/product?p_id=21711) 3D printer, which was used in this side project.

While working on the original full multi-effects board I’d thought it would be cool if I could make a minimalist, super compact, scaled-down, version of the full board. Something that could maintain most of the functionality of the board, in a much smaller footprint; the size of a large guitar pedal. I started tinkering around in TinkerCAD; a free online modeling software to see if I could fit everything in the case, and then be able to 3d print it on my small 200x200x200mm footprint. Based on the dimensions, it seemed this would be possible.

# Parts List

1. [Raspberry Pi 3b+](https://www.amazon.com/CanaKit-Raspberry-Power-Supply-Listed/dp/B07BC6WH7V/ref=sr_1_4?crid=US9NO7N1GCHR&keywords=rasbperry+pi+3&qid=1579269434&s=electronics&sprefix=rasbperry%2Celectronics%2C202&sr=1-4) (Rpi4 would probably work as well) ~\$57

1. [USB Digital Audio Converter](https://www.amazon.com/Plugable-Headphone-Microphone-Aluminum-Compatible/dp/B00NMXY2MO/ref=pd_rhf_ee_s_rp_c_0_3/142-8680092-1752359?_encoding=UTF8&pd_rd_i=B00NMXY2MO&pd_rd_r=c24e9ce6-52c4-494d-9f06-61e1ebc01716&pd_rd_w=F0hKd&pd_rd_wg=AcpCH&pf_rd_p=47aca1ff-ca8a-4580-98d2-db0e7a088eb8&pf_rd_r=ZFFJKG3NWPKK2TNZWXGE&psc=1&refRID=ZFFJKG3NWPKK2TNZWXGE) ~ \$10

1. [USB Hub](https://www.amazon.com/gp/product/B01ID9CADO/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) ~ \$7

1. [Keyboard](https://www.amazon.com/Rii-Ultra-Slim-Compact-Keyboard-Windows/dp/B077P45VND/ref=sr_1_8?keywords=keyboard&qid=1579269204&s=electronics&sr=1-8) ~ \$9

1. [3D Printer ](https://www.amazon.com/Monoprice-Select-Mini-3D-Printer/dp/B07T44GTNQ)(or access to one)~\$220

1. [3 x Momentary Foot Switches](https://www.google.com/aclk?sa=l&ai=DChcSEwi1odHd5IrnAhVGvsAKHYiiBsQYABAiGgJpbQ&sig=AOD64_37SO6KZOVAWtQaD9PEx07E5q8fDA&ctype=5&q=&ved=0ahUKEwi62Mvd5IrnAhVQPq0KHe00BdEQ2CkI4QU&adurl=) ~\$3 each

1. [2 x 1/4" jacks](https://www.google.com/shopping/product/4641846429978408093?q=1/4%22+jack&rlz=1C1CHBF_enUS860US860&sxsrf=ACYBGNQGJU8NZ3RzH6HqMzhQjUILYaaQAQ:1579269373208&biw=1280&bih=649&safe=active&prds=epd:4930003278271589790,paur:ClkAsKraX_lYRSzbfzEdLczGxLQZ-Ad0oaJZHdtR9zVF9S6MIPNJlJr9p68aVI8FvheRzgF8IyNgDBgYa4rz82mJRjLrGLw4JuA_uV_SCu1ykdSp7OEO2QjUORIZAFPVH70-N2rjcDOyC0UsyoOAy2UvSSgeag,prmr:1&sa=X&ved=0ahUKEwikwYDy5IrnAhVFMqwKHbV8Aq0Q8wII9AI) ~\$0.50 each

**Total:** \$93.00 _(excluding 3d printer)_

To put this price into perspective, a “dumb” guitar pedal such as the [Big Muff](https://www.amazon.com/Electro-Harmonix-Muff-Guitar-Effects-Pedal/dp/B000BQTCDO) that this project enclosure is based around, _can easily range \$100+_. Pedals are expensive y’all.

![](https://cdn-images-1.medium.com/max/2876/1*-27hRu0XFjr62Pf0IpySUA.png)

![](https://cdn-images-1.medium.com/max/1794/1*3iRO7IHWyhKd2rBVf77Aww.png)

![111 was the max I was able to get my printer to print](https://cdn-images-1.medium.com/max/1256/0*dyv5gzbV-XsNPRt1.PNG)

After some time I was able to modify an existing 3d printed guitar pedal design into the size/shape I required. I designed some rails for the pi to be mounted, and then everything else could just be tucked away inside as neat as possible. Obviously I had to come up with a catchy name for such a gadget too: TinyFX

![](https://cdn-images-1.medium.com/max/1256/0*OwIZIdsOqgfmaAVA.PNG)

Here’s the [Thingiverse link](https://www.thingiverse.com/thing:3905056) for those interested!

The concept is very simple, yet works the same at the core as the full pedalboard. Guitarix autoboots on the pi, which gets I/O from a USB DAC, but instead of using 10 different input switches/toggles, there would only be 3. “Next”, “Back”, and “On/Off”, or something similarly named. The “Next” switch, as the name implies, would cycle to the next preset/patch within Guitarix. Conversely, “Back” would cycle back to the previous one. Lastly, “On/Off” would mute/unmute the signal. Next Step, Print it out!

![3D Printed Top /bottom shell](https://cdn-images-1.medium.com/max/1904/1*MQdEm1HjP7SAd5gcOfLmYA.png)

Now that the pieces have printed out, I have my first prototype! The print wasn’t perfect, but at this point, I am still dialing in the settings on my printer. Either way, it works well enough as a PoC. Does everything fit as expected though? I installed the footswitches, and 1/4" input/output jacks, and began assembling the pedal.

![](https://cdn-images-1.medium.com/max/4882/1*Sh2VktznuKsUn6m4yyMBLA.jpeg)

![](https://cdn-images-1.medium.com/max/1200/0*UeufRX_HZIKNDNK6.jpg)

I don’t have a picture of it, but unfortunately, all the components do not fit inside the housing as I’d hoped. This is mainly due to the USB Hub I need to use for the system to work properly. The old keyboard that [I cannibalized to route the footswitches to the hotkeys within Guitarix](https://medium.com/@atippy83/guitarix-the-pi-dle-board-8d6298ca8e42) seems to have trouble with the pi every time it reboots. When I connect the keyboard directly to the Pi, whenever the Pi is powered on, Guitarix will load up as intended, however, the keyboard is not recognized by the pi. The only way I found to get around this was to either unplug/replug the keyboard after each boot; not ideal, or run through a USB hub, which seems to remain recognized through multiple reboots. Hence the need for a USB hub.

For V2 of this project, I’m gonna try to find a small USB hub with a right-angled USB connector. Additionally, I’ve made an updated version of the bottom shell of the pedal that is taller than before. If that fails I may look into directly controlling Guitarix with MIDI or GPIO pins or something, but that’s another project in itself.

![](https://cdn-images-1.medium.com/max/800/0*j9ivPXDS_hGY11SW.jpg)

With the death of my Raspberry Pi3b+, both the pedal and pedalboard are on hold at the moment until I get another one or ADHD hyperfocus strikes again. Until then I’m gonna be printing stupid amounts of Baby Yoda figures.

If you have an idea on how to solve the space issue, I’d love to hear ideas!

Hack the Planet

# Thanks for reading!

Follow me on twitter if you want [@Tibbbbz](https://twitter.com/Tibbbbz)

Check out my [main blog](https://anthonytippy.github.io/)!

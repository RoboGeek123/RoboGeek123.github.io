---
layout: post
title: Risks & Vulnerabilities in Enterprise Audio Visual Systems — Part 3 — Results
---

![alt text](https://cdn-images-1.medium.com/max/800/1*qRcB02EQIQTAXcRUTnPMcA.png)

In my last post, we finally gathered and sorted out the relevant data from my research on various audio-visual devices on Shodan. This post will entail a summary of the research I’ve completed over the past months. Enjoy!

Note: These are the main points of my research. There are other devices and categories of audiovisual equipment that I researched but found to be less critical. If you would prefer to watch the full talk on YouTube, I will be uploading it soon.

**Disclaimer:**

I do **NOT** condone any of these techniques or practices. Do not log into or attempt to access devices that you **DO NOT OWN** or unless you have expressed permission. It is illegal. The point of this research is to showcase how vulnerable audiovisual equipment and systems are in hopes of improving security awareness for companies and manufacturers.

![alt text](https://cdn-images-1.medium.com/max/800/1*ZJTRZD5ittpYXMhzbYOAfw.png)

# IoT Overview
![alt text](https://cdn-images-1.medium.com/max/600/0*oqNI1scACFTbsSFL.jpg)

It’s no surprise at this point that many IoT devices and manufacturers have been the source of many problems and frustrations within the infosec community. IoT manufacturers consistently are late if existent at all to the “infosec game”: Security is commonly the lowest priority in development. As a result, we’ve seen malware for IoT devices skyrocket through the years. What I don’t think many people have considered though is the presence of AV devices within this circle and their potential risk to the enterprises and environments around them. As the two formerly separate worlds of AV and IT have merged closer and closer, there has been a lot of growth in companies that now are faced with IT frameworks. As more and more devices are released with “connected features”, the problem gets larger and larger. Even basic security hygiene and standard practices have yet to be adopted by many manufacturers.

# Default Passwords & Device Settings
![alt text](https://cdn-images-1.medium.com/max/600/0*d6zKsweReAPqMdRU)

As a result of these weak security practices, many devices have problematic and insecure default passwords such as “admin” or “1234; that is if they even have a password enabled at all. Moreover, devices often have unnecessary ports open without overtly informing the end users; ie in the user manual, which few take the time to fully read. Many users and integrators will install the device(s), initialize it, and forget about it until it breaks. Security is often not directly considered. Many research studies have concluded with similar results, “ 15 out of 100 have default passwords (15%)”-The Inquirer

![pic](https://cdn-images-1.medium.com/max/800/0*H1-bNqX0GbbIb-VP)

This is one of the main issues that I found in my research. Default passwords or often **no default authentication** is far too prominent in these devices. Additionally, many ports are open by default such as HTTP/HTTPS web pages, SSH, RTSP, or Telnet, as seen below in a study from [Bleeping Computer](https://www.bleepingcomputer.com/news/security/15-percent-of-all-iot-device-owners-dont-change-default-passwords/).

![pic](https://cdn-images-1.medium.com/max/800/0*bCk62zEMFrhfLc7N)
And this is supported by the data I gathered as well in my research as seen below. As you can see, the top device had 38 ports open. 38! WHY!? Some of these are HTTP Pages, telnet, ssh, or just random dedicated control ports but it’s completely unnecessary to have any more than five opened with a vast majority of these devices

![pic](https://cdn-images-1.medium.com/max/800/1*0PE5PfOFxdnrkXPtcvyL-Q.png)
![pic](vhttps://cdn-images-1.medium.com/max/400/0*mZ-POuTAyi1Ep1Mp)


# Research Overview
As mentioned in previous blog posts, the main focus of my data collection has been devices manufactured by Crestron, AMX, Extron, and Cisco (TelePresence). I was able to visualize the data with [Google Data Studio](https://datastudio.google.com/) and draw conclusions. It should be noted that the data collected below is from September 2018 to January 1st, 2019. I am still gathering data as it pertains such as manufacturer count going forward as well.

![pic](https://cdn-images-1.medium.com/max/1200/1*IufpCkaYnS6cqaIsFVq31Q.png)

The most popular manufacturer of devices found was Crestron; with the top device (Crestron- CP3 Control System) totaling over 4,900 online devices online. Additionally, Crestron made up more than 80% of the spread of devices queried (of an average of 26,369 devices) compared to Cisco TelePresence which only totaled 13% of devices. AMX and Extron devices made up less than 4% of devices.

I didn’t find any specific positive or negative correlation with regards to devices over time but it should be mentioned that the red line of “All Devices” refers to the total data queried from Shodan which included some inconclusive results for TV’s and other unidentified devices. Due to the vast number of “product: TV” results; over 28,000 on average, I have decided to retract that data from my research so far, however, I will most likely dedicate research time to this data set in the future.

![pic](https://cdn-images-1.medium.com/max/800/1*uGYLjQiVhf9dcNMwPVT2dg.png)
![pic](https://cdn-images-1.medium.com/max/1200/1*DgKu7142ZUbH26UAs84s8Q.png)

As seen above, the Cisco SX20 is by far the most popular device in Cisco TelePresence. What’s more concerning is the vulnerabilities that were found in addition to these numerous online devices. I was able to find and gain access to multiple video codecs from Shodan alone **without** entering passwords. Just click a link and *GO*! What could go wrong? Below is the configuration page that telecommunications engineers would use to set up video conferences and recordings.

![pic](https://cdn-images-1.medium.com/max/1200/0*cGgp3LG46FqC67kG)

![pic](https://cdn-images-1.medium.com/max/800/0*_XwL_ViLf3Aygp3R)

![pic](https://cdn-images-1.medium.com/max/600/0*dC3QSr-cAX7-Zag9)

As you can see, these web control pages allow the user to manipulate the video system in many different ways. Specifically, this is the exact page that AV engineers would use to troubleshoot/ make calls/ or update software. And all of it is fully online, unauthenticated, and at your disposal. Why can I as a non-authenticated person access the codec API commands!?

## Put. Passwords. On. Your.Device.Logins. PLEASE!

![pic](https://cdn-images-1.medium.com/max/800/1*Av-hP_SehPt5a5b7Rr4JNg.png)
![pic](https://cdn-images-1.medium.com/max/1200/1*4y26NQds49S7Baxr2FDqhA.png)

Crestron was my largest sample of data at over 21,000 devices on average; sometimes reaching up to as many as 25,000 online devices. As seen above, two devices stand alone as the most popular devices: MC3 and the CP3 controllers. Additionally, it’s worth noting that thankfully, the most common open port is 41794, a configuration port for Crestron Toolbox, a proprietary program to interface with Crestron devices, and not an HTTP/HTTPS port such as 80 or 443. Unfortunately, this isn’t much better for security or peace of mind either.

# CVE-2018–10630 — Passwords!
[CVE-2018–10630](https://ics-cert.us-cert.gov/advisories/ICSA-18-221-01) is a vulnerability discovered by Ricky “HeadlessZeke” Lawshae at [Security Compass](https://blog.securitycompass.com/security-advisory-regarding-crestron-tsw-xx60-touch-panel-devices-9f1a71a926a5). In this vulnerability, Crestron “TSW-X60” Series devices are shipped from Crestron with **no authentication** on the telnet-like control port: 41794. As such, this enables an RCE vulnerability for **ALL** software versions prior to 2.001.0037.00.

![pic](https://cdn-images-1.medium.com/max/600/0*ase3DpndN3yLWsza)
## Models Affected

- TSW- 1060
- TSW- 560
- TSW- 760
-MC3 Master Controllers
As you can see below, my research uncovered a lot of “X-60” touchpanels open to the internet. What is really concerning is that only 10.5% of these touchpanels were updated to the aforementioned firmware version.

![pic](https://cdn-images-1.medium.com/max/600/0*jFUWmrFhzd-aQYyi)

![pic](https://cdn-images-1.medium.com/max/1200/1*lhDb7AozmpYT3jeiksh4pw.png)

## REMINDER: UPDATE YOUR FIRMWARE PLEASE!

![pic](https://cdn-images-1.medium.com/max/800/1*GFxfFmwktXPyWJ4em6K9JA.png)
![pic](https://cdn-images-1.medium.com/max/400/0*CH89Bvpf9Dhy5qZs)

# But wait… THERE'S MORE…
Crestron offers users web control for many of there devices. Unfortunately, many devices **ship without any authentication enabled**…so anyone can access and modify settings…such as firmware version. So in effect, even if you do have updated firmware and are not vulnerable to a current vulnerability if you don’t have a password on your web configuration page, then any bad guy can downgrade the firmware to a vulnerable version.

![pic](https://cdn-images-1.medium.com/max/600/1*cApmL7PYEQtD9g6QsIk6dw.png)
![pic](https://cdn-images-1.medium.com/max/600/1*12Aoef3VEocxPSBNhGS3TQ.png)

“But surely the NEWER models offer better security riiiight? Nope. Still able to access the web configuration page. New face, same risks.

![pic](https://cdn-images-1.medium.com/max/1200/0*8gCWMhEKZg_lJf6X)

If you think that’s bad, [Ricky “HeadlessZeke” Lawshae](https://twitter.com/HeadlessZeke) demonstrated the destructive potential of vulnerabilities in audiovisual systems at [DEFCON 26](https://youtu.be/BNAqdEpsYxc?t=1881). In his research, he was able to break out of the Crestron “sandbox” using a script and get root access to a bash shell on the touch panel remotely.

![pic](https://cdn-images-1.medium.com/max/800/1*MsJ255aXouJd5UqydECj6w.gif)

And in addition to getting a root bash shell on the MC3 master controller, he was able to run a script to enable an RTSP stream from the touch panel using the onboard camera and microphone; essentially enabling a private spying stream to the area around the touch panel. It should also be mentioned, that when he executes either of these scripts, nothing changes on the touch panel to alert the user of what is happening behind the normal operations. Did I mention that these touch panels are widely used in hotels, airports, universities, and even government applications?

![pic](https://cdn-images-1.medium.com/max/1200/1*xS24gLzqvQ9E7LOGZ3y9tg.gif)

Vulnerabilities, Botnets, and Cryptominers OH MY!
Lastly, it is also likely that your touch panel or master controller could be part of an IoT botnet. Yep, IoT botnet. Multiple touchpanels that I investigated attempted to transfer this file on my machine upon connection…
![pic](https://cdn-images-1.medium.com/max/800/0*5ALWfqru8I0fvSTB)

# What is “Photo.scr” you ask?
The **Photo.scr Miner** is a Trojan that utilizes a victim’s computer processing power to mine the digital currency called Monero. When installed, this Trojan will install two monero different Monero miners called acnom.exe and acnon.exe that will attempt to mine Monero for the malware developer by using the resources of your computer’s processor.

![pic](https://cdn-images-1.medium.com/max/600/0*YPCNoEpUHe30Upb7)


# Crestron Air Media
![pic](https://cdn-images-1.medium.com/max/600/0*NMVI9x26jpI9FZ2E)

Another area research within Crestron devices was Air Media; a wireless presentation solution similar to Google’s Chromecast. In the same form as other Crestron products, Air Media devices have a web configuration page that is enabled by default. Additionally, AM-100's; or the first version (compared to AM-200 or 300), do not have authentication enabled by default. So as with far too many other devices, if you know the IP address, you have access to the full control panel…

![pic](https://cdn-images-1.medium.com/max/600/0*iSFlML-P2fvFwOl1)
At the very least, this provides the opportunity for stereotypical “hacker mischief” commonly seen movies, if not a serious security vulnerability to the companies who host and operate these devices. For example, to connect to an AM-100 you would access a page similar to the to this.

![pic](https://cdn-images-1.medium.com/max/600/1*eweKVruQSKS8fUW9itUWFQ.png)

Then you would be greeted with a page similar to this to connect. As you can see, in order to “authenticate” users, Air Media devices deploy a 4 digit code located in the top right corner. BUT, if you have access to the web configuration controls, then you can just disable it.

![pic](https://cdn-images-1.medium.com/max/600/1*RQMEkMcF8o9FNyYWvGsv4Q.png)

And once disabled, you can connect and stream anything you’d like to the device; and ultimately to whatever that device “feeds” such as TV’s, displays, projectors…etc.

**Which could result in…**

![pic](https://cdn-images-1.medium.com/max/800/1*ZL9xWWTgG03qOpjsTDGNNA.png)

![pic](https://cdn-images-1.medium.com/max/800/0*NjFqYLxJkkS1e2Wl.png)

![pic](https://cdn-images-1.medium.com/max/1200/1*sTOXuy_FEURMdzyKaSSBxA.png)

I wasn’t able to glean as much information from AMX devices as I could with other manufacturers such as Crestron due to HTTP header content and structure. Specifically, other devices such as Crestron or Extron devices have serial number, model, and firmware version right in the HTTP header; which Shodan harvests. It is worth noting that port 23 (telnet) was the most common in AMX devices and additionally, there seems to be a slight increase in devices online. But don’t be fooled by these numbers, AMX devices are still used widely in enterprises and other organizations worldwide. I suspect that this isn’t the full list of AMX devices due to obscurity of the HTTP header information.

![pic](https://cdn-images-1.medium.com/max/600/0*UopRzqs-XXgCdEg-)

# ICSA-16–049–02A — Backdoor Accounts!

>“The usernames “1MB@tMaN” and “BlackWidow” were hard-coded in the firmware and allow for remote login in debug mode, granting the ?>attacker access to tools not provided to administrators such as packet sniffing.”-ics-cert

But, just like any devices, AMX devices are not free of vulnerabilities. Backdoor accounts were embedded in the code by AMX employees for testing and debugging and have elevated privileges to configure and modify.

![Pic](https://cdn-images-1.medium.com/max/600/0*cO_3Uwt9DSj_VCx2)

## Products Affected

* NX Controllers
* DVX Series
* DGX Series
* NI series

This vulnerability is similar to the Crestron TSW/ MC3 vulnerability over the telnet like a client. Users can access these devices and send arbitrary commands as they see fit.

# AMX Web Control- Unauthenticated

![pic](https://cdn-images-1.medium.com/max/600/1*9tP3-FiFeuZZHdm3C6XDkQ.png)

Unfortunately, I found far too many touch panels that don’t even require technical skill to access. Similarly to the Crestron TSW touch panels, some AMX touchpanels have web pages for web control. Fortunately, unlike some control pages, I was not automatically logged under admin privileges. However, what I discovered was almost worse. I was granted “guest” privileges with seemingly admin level access to controls. I could issue strings and commands to the master controller directly from the web page.

![pic](https://cdn-images-1.medium.com/max/600/0*AftOsU1FyHv35urU)
![pic](https://cdn-images-1.medium.com/max/600/0*GbLO-cwaEqBjDgJf)

For whatever reason, even though I was “logged in” (Note: I never completed any log-in prompts), I had nearly full access to any controls or configurations that I pleased. What could go wrong? Why is this a guest account privilege?

![pic](https://cdn-images-1.medium.com/max/800/0*0K8T-YiTWHCr7Li8.png)

![pic](https://cdn-images-1.medium.com/max/1200/1*ucMZGG5HncxWAc7HUi8yRA.png)

Despite not finding a lot of devices online, Extron devices proved to be rather interesting to research. One trend I found was that many devices that provided an HTTP page were unauthenticated and open for anyone to look at or control. As in aforementioned devices, all I had to do was find IP’s with HTTP ports open and visit the IP address. I was able to gain default admin access to many devices such as the switcher below using this method. Why are these here!? Why aren’t they secured?!

![pic](https://cdn-images-1.medium.com/max/1200/0*p4MXKloBwD16qHfT)

I had similar experiences with Extron controllers and control systems as well…

![pic](https://cdn-images-1.medium.com/max/800/1*clkizbnjomIoUp3pB-WQpA.png)


And lastly, my favorite device that I found was the SMP series media processors. These devices are used to capture and store video recordings or screen captures of content. Similarly to other Extron devices, I was able to start and stop recordings, start streams, change resolutions…etc. Even more so, I was able to enter “preview mode” for the content being shared; which in this case was a camera feed with content. All from the click of a link, without ANY logging in. I could even have downloaded content from their “secure” FTP server using “admin” or “user” credentials…which were not applied. So come right in I guess.

![pic](https://cdn-images-1.medium.com/max/600/0*ncHRPftLU4stctBb)
![pic](https://cdn-images-1.medium.com/max/800/1*48jTBtgr6DFamr0AWKeoBQ.png)
![pic](https://cdn-images-1.medium.com/max/400/1*zbNIdfCGOQvCSkTrawbqNg.png)

# Most Vulnerable Organizations- Breakdown
![pic](https://cdn-images-1.medium.com/max/1200/1*UGDly2RyU-DtiwGqb822CQ.png)

One of the most interesting conclusions I made from the data was that most of the devices came out of private ISP’s and not colleges or universities. I did indeed find many many universities with devices that were open facing, but this isn’t just a “university problem”. These security risks seem to span to both private and public sectors.

## At Risk Organizations
* Understaffed/ Inexperienced AV/ IT Teams/ Integrators
* Universities
* Small Businesses
* Existing Legacy equipment

![pic](https://cdn-images-1.medium.com/max/600/1*NF4P2iXhrWGLkTrdnN6gzA.png)

# How do we better secure our organizations?
![pic](https://cdn-images-1.medium.com/max/800/0*HCKXYdECXWwdqTJk)

# A. Basic Security Hygiene
1. CLOSE YOUR FIREWALLS PLEASE GOD STOP PUTTING DEVICES ONLINE!
2. Default authentication
3. Disable unnecessary ports and features
4. Consistent firmware upgrades with a network device manager
5. Physically secure technology in a locked rack

![pic](https://cdn-images-1.medium.com/max/800/0*TRjeL9vSL1tqgPpJ)

**First** and foremost, you should ensure your router isn’t port forwarding or exposing any devices to the open internet. This should be your first and foremost priority in evaluating these devices. All of the devices that I found have no reason to be on the internet. WHY **GOD WHY** do you need to monitor your 10 channel switcher or control panel over the internet? You don’t, you really don’t. You’re making A/V guys look bad. Please stop it.

![pic](https://cdn-images-1.medium.com/max/600/0*ga7cHiDxgULuzKUw.jpg)

**Secondly**, if you absolutely HAVE TO put your device(s) online, then please make sure they’re secured by a non-default password. As mentioned above in multiple devices, many manufacturers ship devices with many default “features” enabled and default passwords enabled. Before you “go live” and implement any of these devices, ensure that the password has been changed to a secure password.

![pic](https://cdn-images-1.medium.com/max/600/0*uo_hpLltsYhRHUDZ.jpg)

It is often lamented that security is often overlooked, underfunded, or underprioritized which brings me to my third point: As an Audio-Visual provider/ supplier it is **always** a good idea to make security a focal point of your operations just as you would with more traditionally “mission critical” focuses. The current state of IT is such that you must be vigilant in maintaining a security-focused product or solution to mitigate risk and harm to your organization and your customers. In doing so, you can rest easy knowing that you aren’t opening up your customers to risk by shipping them conference room designs or configurations with gaping security holes that could have been prevented. I’m not a sales guy by any stretch of the word, but your customers and clients will thank you for the effort. It is well worth every bit of effort.

![pic](https://cdn-images-1.medium.com/max/600/0*HAqLCsie5JK2k_ua.jpg)

I’ve said it once already, and I’ll say it again: Update your firmware! Firmware updates are critical for these devices. Primarily for operation and mitigation of bugs and glitches which results in better uptimes, but as mentioned before, security. The task of updating firmware for devices can pose a huge challenge, especially when completed by a smaller team. Consider that your team manages audiovisual support for a large enterprise. Your team is responsible for managing and servicing over 500 conference rooms of various capabilities. The task of upgrading and maintaining firmware on all of these rooms and devices is quite taxing on top of maximizing room uptime and handling your teams regular workload. On one hand, you could manually upgrade the firmware with each visit, or you can utilize a device management suite such as Crestron Fusion or Cisco Unified Communications Manager (CUCM) to push out firmware to hundreds of devices with one click regardless of scale. Additionally, you can measure and report metrics on individual devices, and even change passwords or download system logs. Device Managers save time, reduce risk, and maximize uptime for minimal costs.

![pic](https://cdn-images-1.medium.com/max/600/0*qDBYq-yKhH0jjb5M.png)

Lastly, in regards to the physical side of security, it is encouraged to store equipment in racks with locks. This will not only prevent any malicious actors from physically compromising the device; such as placing bugs, downgrading firmware…etc, but also prevent end users from trying to “fix” issues. Believe me, your support team will thank you greatly if the equipment is physically secure from any harm or foul play.

# Documentation — Your Best and Worst Friend
From a malicious actors perspective, the “best” part about many of the risks associated with these devices is the wealth of documentation such as user manuals, programming guides, and setup guides are often widely available to anyone who searches for them. Even if passwords were implemented in devices, many of them are sure to be the default password which can be found with a quick google search. For example, for many of these devices, I was able to find default passwords in under 5 minutes by CTRL-Fing (searching) through user manuals for “default password” or “admin”. In under an hour, I had the default passwords for a number of popular devices as well as documentation for features and other pathways that I could try to exploit. As mentioned above, I did not specifically “log in” to any of these devices or brute force access, however, I don’t believe it would be much of a task at all to obtain access using such methods.

B. Advanced Security Tips
1. Subnet your devices (Data over here/ Control over there)
2. Enable encryption on communications
3. Include AV devices within your IPS/IDS system
4. Security integrated into the development /planning process — Manually vet and research devices with security team before implementation
A common practice for securing devices even outside of audiovisual equipment is to utilize subnetting, or multiple sub-networks for specific network traffic. In other words, you can have personal data and financial documents on Network A, and device control data on Network B. This practice is often used in SCADA systems such as power control centers and is often very effective at restricting access to unauthorized users. It should be noted that this a more “advanced” strategy but it is very effective.

# C. Manufacturers — What Can You Do?
**Security by default/Design — Zero Trust Policy**
![pic](https://cdn-images-1.medium.com/max/600/1*WO-KvLtKgMmJgz1aQJNePA.gif)

* It should **NOT** be the user's full responsibility to be security experts. We need to share the responsibility
* No more uniform default passwords for devices (California is enacting this to law by 2020)
* Disable any unnecessary ports by default
* HTTP web interfaces **need** passwords
* Automatic firmware updates (need device manager)
* Triggered alerts upon outage or error
* Audit logs enabled by default

# Conclusion
In 2019, many audiovisual devices still have weak and outdated security practices that open themselves up to considerable risk of data loss or damages. Much of this risk is attributed to default configuration settings such as default passwords, ports, and other “features”. It is my firm belief that manufacturers and consumers alike need to take a more aggressive step together towards mitigating risks in IoT devices by leaning into and learning about basic security hygiene to better protect the organizations they are operating in.

# Thank You!

![pic](https://cdn-images-1.medium.com/max/600/1*DnDyYN3E9t50nn4Iu30bZw.gif)

Many many thanks to my amazing wife for supporting me through my many “rabbit hole” nights of huddling over my computer until 3 am. Thank you to #misec for the many encouraging words and for helping me refine my research. Lastly, thank you to the amazing InfoSec community at GrrCon for sparking my interest and inspiring me to research this topic in the first place.

# Next Steps?
I am currently working on project that will interact with the Shodan API and gather query data of specific searches on a recurring and automated pattern. In otherwords, I would have much better visibility into potential trends of online devices if I could get the counts of Crestron, Cisco, Extron, AMX , and other devices EVERY day for the span of a year; instead of every Friday for a couple months. Additionally, as mentioned above, I will be looking into the vast numbers of Samsung and LG smart TV/ displays online. This was recently showcased in an “educational” hack by HackerGiraffe on twitter. The so called “CastHack” exploited thousands of chromecasts, roku devices, and smart tv’s which just shows how widespread this issue is.

# Bonus: You’re Really Still Reading This!?
## Crestron PYNG- HUB Smart Home
![pic](https://cdn-images-1.medium.com/max/600/0*3xDylFaV7ZPW3WpC.png)

In the course of my research for each manufacturer, I occasionally found devices that were not specifically “Enterprise AV”. For example, Crestron offers many control systems for non-AV applications such as the PYNG-HUB; a smart home hub. Unfortunately, many of the above risks prove true with the PYNG-HUB as well.

![pic](https://cdn-images-1.medium.com/max/600/0*BP9ORkMtTdrdZz1b)

As with many other Crestron devices, I was able to access a webpage to control the device but since PYNG-HUB is a smart hub, the page I accessed was an emulation of the touch control panel for the house… And there’s A LOT of them online. What could possibly go wrong?

![pic](https://cdn-images-1.medium.com/max/600/0*EkYqAeUhLo5kdVI8)
![pic](https://cdn-images-1.medium.com/max/600/0*8q6Sro3ohKgrY5Fy)

*This is the touch panel I was greeted with upon visiting the IP address provided by Shodan. Full unauthenticated control to someone’s SMART HOME. Fortunately, it appears that this control system only controls the lights. But if I were a malicious actor, this could provide a wealth of information on my target.*

As if this wasn’t bad enough, after exploring the reaches of the panel for a bit I stumbled upon a link, which took me to a report page for metrics about the house including lighting costs, times, and even thermostat data if connected.

![pic](https://cdn-images-1.medium.com/max/800/1*5zDqwCsabD0v-5CTZkTfKg.png)

# Thanks for reading!


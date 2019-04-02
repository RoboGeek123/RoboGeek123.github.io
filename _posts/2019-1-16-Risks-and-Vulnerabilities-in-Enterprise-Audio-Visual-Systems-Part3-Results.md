---
layout: post
title: Risks & Vulnerabilities in Enterprise Audio Visual Systems — Part 3 — Results
---

![alt text](https://cdn-images-1.medium.com/max/800/1*qRcB02EQIQTAXcRUTnPMcA.png)

# CURRENTLY UNDER CONSTRUCTION

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

-TSW- 1060
-TSW- 560
-TSW- 760
-MC3 Master Controllers
As you can see below, my research uncovered a lot of “X-60” touchpanels open to the internet. What is really concerning is that only 10.5% of these touchpanels were updated to the aforementioned firmware version.

![pic](https://cdn-images-1.medium.com/max/600/0*jFUWmrFhzd-aQYyi)

![pic](https://cdn-images-1.medium.com/max/1200/1*lhDb7AozmpYT3jeiksh4pw.png)

## REMINDER: UPDATE YOUR FIRMWARE PLEASE!

![pic](https://cdn-images-1.medium.com/max/800/1*GFxfFmwktXPyWJ4em6K9JA.png)
![pic](https://cdn-images-1.medium.com/max/400/0*CH89Bvpf9Dhy5qZs)

















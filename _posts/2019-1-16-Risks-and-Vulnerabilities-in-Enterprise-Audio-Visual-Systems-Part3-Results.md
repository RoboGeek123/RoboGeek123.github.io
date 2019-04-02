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

#IoT Overview
![alt text](https://cdn-images-1.medium.com/max/600/0*oqNI1scACFTbsSFL.jpg)
It’s no surprise at this point that many IoT devices and manufacturers have been the source of many problems and frustrations within the infosec community. IoT manufacturers consistently are late if existent at all to the “infosec game”: Security is commonly the lowest priority in development. As a result, we’ve seen malware for IoT devices skyrocket through the years. What I don’t think many people have considered though is the presence of AV devices within this circle and their potential risk to the enterprises and environments around them. As the two formerly separate worlds of AV and IT have merged closer and closer, there has been a lot of growth in companies that now are faced with IT frameworks. As more and more devices are released with “connected features”, the problem gets larger and larger. Even basic security hygiene and standard practices have yet to be adopted by many manufacturers.

#Default Passwords & Device Settings
![alt text](https://cdn-images-1.medium.com/max/600/0*d6zKsweReAPqMdRU)


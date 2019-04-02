---
layout: post
title: Research Project- The Start
---
![alt text](https://cdn-images-1.medium.com/max/800/1*xWkt20O4nsI56U9T7Uu-Tg.png "Research Project Part 1")
# The Beginning
A couple of years ago, I began to take a strong interest into Cyber Security. I started pursuing the field through DEFCON talks, youtube videos, and articles about this fascinating new world. It didn’t take long before I became connected with a local group — [#misec](https://www.misec.us/); a Michigan based Cyber Security / IT professional development group.

I quickly took to this new community of professionals and friends who encouraged me to continue feeding my hunger to learn more. And as is often the case in IT, the more I learned, the more questions I gathered. Fast forward a bit, and everyone’s talking about this convention that just happened — [Converge](https://www.convergeconference.org/): Detroit; a Detroit Cyber Security conference. Disappointed that I had just missed it, I started looking for the next con — [GrrCon](http://grrcon.com/); of Grand Rapids. I requested the time off work and eagerly looked forward to my first real convention.

![alt text](https://cdn-images-1.medium.com/max/800/1*py67isk45NBgH5EfuV59Gw.jpeg)
![alt text](https://cdn-images-1.medium.com/max/400/1*JO9EBb8J9lsAS4JZN_xU5A.jpeg)

# The Conference

With a tinge of anxiety and full of excitement, I headed up to Grand Rapids to discover an incredible conference full of people whom I had chatted with on the #misec slack channel as well as other cyber security and IT professionals. Finally, I had really found my people. I was surrounded by people who had the same interests, got the same jokes, and had the same curiosity for technology as me. And just like me, they wanted to learn how things worked. They loved tearing into devices to see the guts and inner workings. By the end of this incredible conference, I was inspired, felt at home, and was eager to break ground into some research to continue my learning. After all, what better way to learn something than to jump right in right? So I set out a goal for myself — -I would write a talk on SOMETHING. *dun dun duuuuun*

I knew I wanted to research and develop a talk, but ON WHAT. At this point, I’m still really new in Cyber Security. I know just enough to get myself in trouble. But, I DO have a lot of experience with Audio Visual Systems and equipment. So, after much deliberation and forethought, I chose my point of research: **Risks & Vulnerabilities in Enterprise Audio Visual Solutions.**

# The Beginning of Research — A bit more than I can chew?

With my newfound topic heading and some years of experience as an Audio Visual Support Technician, I set out to research vulnerabilities in audio visual solutions found in large businesses across the world. I distinctly remember thinking to myself: *“There can’t be that much right?”. “I bet all the cool vulnerabilities are all patched up”.* Was I ever wrong…

![alt text](https://cdn-images-1.medium.com/max/1200/1*u0WDtwKu-F8I4VW7_UqbVg.png) ![alt text](https://cdn-images-1.medium.com/max/600/1*8AlD7kvXptUMkl0YuNpqFg.png)

I discovered the absolute firehose of information on the internet known as [Shodan](https://www.shodan.io/explore) and began searching queries involving popular audio-visual devices and manufacturers that I’m familiar with. If you’re not familiar with Shodan, it’s a search engine for IoT connected devices. Essentially, if it reaches out to the internet, it’s probably somewhere on Shodan. After many searches using just the web GUI, being limited to the Shodan’s parameters, I chased after more. I created a student account; free with a .edu email address FYI and was able to access a much greater spread of features than before. Perfect, now I could use filters such as “port:80” and “Product: Crestron” to look deeper into the results. To say I was surprised at the amount of “low hanging fruit” with these devices was an understatement. It seemed to be limitless. Unnecessary ports open, unauthenticated admin web GUI’s, and other bad security hygiene. I found smart homes, conference rooms, video conference systems, tens of thousands of indecipherable AV products and devices, and so so much more than I had anticipated.


I began downloading data query files with tags such as “AMX”, “Crestron”, ”Extron”, and “TV” hoping to find some devices that I could poke and research to gain further understanding. And I did just that. All in total, I had upwards of 70,000 online devices of some kind.

It was at this point that I came across my first real hurdle my research project: Parsing and Normalizing the Data — Making sense of the noise.

Read [Part 2 — Cleaning The Data](https://robogeek123.github.io/Research-Project-Part-2-Cleaning-The-Data/)

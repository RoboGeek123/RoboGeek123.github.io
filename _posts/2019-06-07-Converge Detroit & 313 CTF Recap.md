![](https://github.com/AnthonyTippy/Images/blob/master/Converge%20CTF.png?raw=true)

2019 was my first year attending Converge Detroit, and my second security
conference ever! I had an absolute BLAST! It was so nice to catch up in person
with some of the [#misec](https://www.misec.us/) folks that I’d been chatting
and developing friendships with over the past 6 months. Additionally, I competed
in my very first in-person CTF!

Here are the final results from the [313 CTF](https://0xc7f313.com/leaderboard).
The “A Team” was disqualified as they were conference organizers, so
*technically, *Team Rubber Ducky took 3rd place! And for a team that is mostly
comprised of memes, that’s not bad.

![](https://cdn-images-1.medium.com/max/720/1*9FZE0ixakC2a5Fr1i6FSsQ.png)

Congrats to the winners of the CTF and well done to everyone who participated.

*****

### **CTF-Writeup**

Among my 3 compatriots of the Rubber Ducky tribe, I was able to complete 10
challenges, amassing a total of 69 points ( ͡° ͜ʖ ͡°) Due to my relatively
non-infosec skilled background I shied away from some of the more technical
challenges, but found more than enough challenge in the more “non-technical”
challenges.

*****

### **Locks**

I was able to crack…

* 1 pin lock (1 point)
* 2 pin lock (2 points)
* 3 pin lock (3 points)
* 4 pin lock (4 points)
* A non-point Kwikset door lock! (Personal victory points)

Totaling 10 points from locks alone! Not too bad for a novice lockpicker!

*****

### **Encryption & Encoding**

#### 1. A long expected party (3 Points)

> “K5UGC5BAMNUGC4TBMN2GK4RAONQWSZBMEARESIDEN5XCO5BANNXG65ZANBQWYZRAN5TCA6LPOUQGQYLMMYQGC4ZAO5SWY3BAMFZSASJAONUG65LMMQQGY2LLMU5SAYLOMQQESIDMNFVWKIDMMVZXGIDUNBQW4IDIMFWGMIDPMYQHS33VEBUGC3DGEBQXGIDXMVWGYIDBOMQHS33VEBSGK43FOJ3GKLRC”

If you decode the above text with a base 32 decoder, it results in:

> What character said, “I don’t know half of you half as well as I should like;
> and I like less than half of you half as well as you deserve.”

A quick google search of the quote reveals that Bilbo Baggins says this in
L.O.T.R. -The Fellowship of the Ring, hence the name *“A long expected Party”.*

So the flag = **Bilbo**

#### 2. Poeseur (5 Points)

“A good glass or a bishop’s hostel might help you find the flag”


> “5;5-?()‡(:305–8;48)8¶5(6‡?)9‡†8)‡1-‡);(?-;635–6.48()889;‡45¶8
> 52‡?;;489556(‡16)-(?;5208)8-(8-:6;5..85()509‡);569.‡))62606;:
;‡?(6††08]45;45)288.?;;‡38;48(2:)‡-‡9.08¢598;4‡†¢¢10536)95(36
5065¢¢5†;‡)‡98.8()‡);48†6116-?0;:9634;283(85;2?;;‡‡;48();‡;4‡)
8)76008†6†8–6.48(63)?-486395)5(8¶8(:)69.086†88†8†35(5005.‡8”

![](https://cdn-images-1.medium.com/max/540/1*yYLvw8tKF9--S5qValbnTw.png)

Clearly, this is text is eligible. Not base 64,32, or any other I could find. I
wonder what it could be? I google searched *“A good glass or a bishop’s hostel”
*which led to “The Gold-Bug” by Edgar Allen Poe (Hence *Poeseur*). The Gold-Bug
is a famous piece which contained a cipher by Poe himself.

After running the original text through a [Gold Bug Cipher
decoder](https://www.dcode.fr/gold-bug-poe), it results in:

> “ATACURSORYGLA–ETHESEVARIOUSMODESOFCOSTRUCTIGA–IPHERSEEMTOHAVE
> ABOUTTHEMAAIROFISCRUTABLESECRECYITAPPEARSALMOSTAIMPOSSIBILITY
TOURIDDLEWHATHASBEEPUTTOGETHERBYSOCOMPLEXAMETHODXXFLAGISMARGI
ALIAXXADTOSOMEPERSOSTHEDIFFICULTYMIGHTBEGREATBUTTOOTHERSTOTHOS
ESKILLEDIDE–IPHERIGSUCHEIGMASAREVERYSIMPLEIDEEDEDGARALLAPOE”

Still not exactly what we want, but at least we can see words. Let's try to
break it up a bit.

> “AT A CURSORY GLA–E THESE VARIOUS MODES OF COSTRUCTIGA –IPHER SEEM TO HAVE ABOUT
> THEM A AIR OF ISCRUTABLE SECRECY IT APPEARS ALMOST A IMPOSSIBILITY TOU RIDDLE
WHAT HAS BEEPUT TOGETHER BY SO COMPLEX A METHOD XXFLAG IS MARGI ALIA XX A D TO
SOME PERSOS THE DIFFICULTY MIGHT BE GREAT BUT TOO THERS TO THOSE SKILLED
IDE–IPHERIG SUCH EIGMAS ARE VERY SIMPLE IDEED EDGAR ALLA POE”

Some letters appear to be missing but we can extract the general idea of what
the text says. More importantly, we note

> XX FLAG IS MARGI ALIA XX

Unfortunately, Margialia doesn’t seem to be the correct flag. I tried upper,
lower, and every case combination with no avail. Finally, I decide to google
search “Margialia” which google corrected to *“Marginalia”*
![](https://cdn-images-1.medium.com/max/720/1*GBPFNrmV2ixTIB1AQJtSPQ.png)

At last! Flag = **Marginalia**

#### 3. Dolar Sit Amet (3 Points)

> “TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdCwgc2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWduYSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1YXQuIGZsYWcgaXMgbG9yZW0gaXBzdW0uIER1aXMgYXV0ZSBpcnVyZSBkb2xvciBpbiByZXByZWhlbmRlcml0IGluIHZvbHVwdGF0ZSB2ZWxpdCBlc3NlIGNpbGx1bSBkb2xvcmUgZXUgZnVnaWF0IG51bGxhIHBhcmlhdHVyLiBFeGNlcHRldXIgc2ludCBvY2NhZWNhdCBjdXBpZGF0YXQgbm9uIHByb2lkZW50LCBzdW50IGluIGN1bHBhIHF1aSBvZmZpY2lhIGRlc2VydW50IG1vbGxpdCBhbmltIGlkIGVzdCBsYWJvcnVtLg==”

When ran through Base64 decoding, it returns

> “Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
> incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
flag is lorem ipsum. Duis aute irure dolor in reprehenderit in voluptate velit
esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.”

From best I can tell, this appears to be Latin, so to Google translate we go!
![](https://cdn-images-1.medium.com/max/720/1*KZqL8v7F1ibb94wGMEV3Mw.png)

Flag =** lorem ipsum**

#### 4. I hear you like QR Codes (18 Points)

> Yo Dawg, I heard you like QR code challenges, so made some QR codes in this
> challenge so you can QR while you QRing.

> So … ya your going to want to loop here.

> File:
> [qr.png](https://0xc7f313.com/lift/ajax/F828314976750KAJQER/?F828314981121JHBLCN=_)
(SHA1: cefbb206c717169174b69d7a27b8968460c2644d)

Ok to be fair, *I didn’t solve this one.* The credit for solving this
monstrosity can only go to the incredible
[@Greenjam94](https://twitter.com/Greenjam94), but as an unofficial member of
Rubber Ducky, he used my account to submit this challenge.

I do not know specifically how he solved this beast of a challenge, but from
what I gather, each QR code was another hint to the *real *QR code which
contained the flag. After much hair pulling and frustration, he came to the clue
of “*X marks the spot” *from an organizer of the CTF.

Apparently, the *intended *way of solving this challenge was to write a script
to break the 1000+ lines of code and process each one uniquely in a loop…while
also not frying your CPU. Luckily, we didn’t end up doing that.

“*X marks the spot” *boils down to X being the ascii to octal for 130. AKA the
130th QR code is the one!

**Note**: I was informed later by the organizer that all QR codes are base64 of
strings, 999 are inspirobot quotes once decoded. Only one of them is the flag.

Flag=**YouCallThisArcheology?**

So there are two ways to solve

1.  one loop to go through the picture and cut up the picture into individual QR
codes
1.  read the QR code and decode the base64

As I said, we got lucky on this one by getting the hint *“X Marks the spot”*

### 3. Who Knows? (7 Points)
![](https://cdn-images-1.medium.com/max/540/1*mOsAlEnJC6Atc_MCEzaYGQ.jpeg)

This cipher drove me NUTS! I stayed up after the first day of the convention
trying to solve it based on [this decoding
solution](https://i.pinimg.com/originals/ff/95/cf/ff95cf3e3db163a6370340b969e37abf.gif)
however it was not correct.

After many hours of descending into madness over this code, I gave up and went
to sleep.

Luckily, *I get by with a little help from my friends. *The next day, my friend
(Thanks [@gondrith](https://twitter.com/gondrith)!) had figured it out and clued
me in on the solution. This cipher was REALLY creative.

As it turns out, this cipher was from a 1930’s popular superhero named “*The
Shadow”. *The Shadow used a “*Chain of Death”* cipher.
![](https://cdn-images-1.medium.com/max/720/1*QZ2BU-AgDDQXH1RiLPWkIw.png)

I was close to the solution, but missing ONE critical key: Rotation. The way you
decode the Shadows Death Cipher is by following the symbols left to right until
you hit one of these symbols

![](https://cdn-images-1.medium.com/max/720/1*vD07UNgyEhXYCw1xusBlaA.png)

At which, you turn the whole document so that the symbol in question is facing
upwards. Then continue decoding. In doing this, it changes what the symbols
decode to.

> “Who knows what evil lurks in the hearts of men Flag is **SHADOW**”

#### **4. Social Media**

> Tweet @0xc7f313 for a flag! Your DMs must be open.

I tagged @0xc7f313 in a post encoded in all hex explaining my love for them and
trying to butter them up. It worked. Butter was deployed. Flag gained.

Flag = **Brawndo**

#### **5. ASL (15 Points)**
![](https://cdn-images-1.medium.com/max/540/1*HdhrPWMf2-2D1EOHfTE9QA.png)

ASL is obviously an American Sign Language challenge. The challenge includes
File:
[ASL.mp4](https://0xc7f313.com/lift/ajax/F8283149024464JGVFK/?F828314937547E3YDRZ=_)
(SHA1: 057a1e810aee44cf626cf8655167f7d7ca0966e6), which is a video of someone
speaking in ASL. Unfortunately, I do not speak ASL, however, a friend of mine
was able to assist (more like carry) me in solving it #Friendship (Thanks
[@vajkat](https://twitter.com/vajkat)!)

Flag = “**alphabet**”

I completed a couple of other challenges as well, but don’t recall exactly which
ones those were or how I solved them. I’ll try to do a better job documenting my
solutions next year.

### Conclusion

Anyways! I would *highly* recommend you go check out Converge Detroit next year
if you are looking to get into information security, or are just interested in
IT in general. There’s a great wealth of information and support from the
community that will be more than happy to help you and teach you along the way.

Read stuff, learn stuff, practice stuff. Hack the planet!
![](https://cdn-images-1.medium.com/max/720/0*DxJtGpr44RBeaXcz.gif)

Wanna continue reading? You can read more [writeups of other
challenges](https://ctftime.org/event/807/tasks/) or check out the[ 313CTF
leaderboard](https://0xc7f313.com/challenges).


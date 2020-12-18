
![source: [https://postpressmag.com/wp-content/uploads/automation.jpg](https://postpressmag.com/wp-content/uploads/automation.jpg)](https://cdn-images-1.medium.com/max/2000/0*G1ogXtXejDXoeWKw.jpg)

### **A/V Device Administration: The old way**

Any onsite managed services (OMS) team interacting with A/V devices in a corporate environment is probably familiar with the struggle of efficiently administering and properly tracking assets or devices throughout corporate networks. Any IT team worth their salt should have reference to what devices are on their network for both device performance and security. Naturally though, when you scale this up to hundreds or thousands of devices it can get pretty tasking to manage especially considering many organizations don’t have dedicated OMS teams for A/V.

![Example web gui screen](https://cdn-images-1.medium.com/max/3154/0*jsxRV5hpt2kWzFgq.png)

Many A/V devices have web interfaces for remote management, which although helpful, isn’t as effective when scaled up to hundreds or even thousands of devices on a large corporate network. For example, say you are tasked by management with gathering the device info from devices in conference rooms/on your network (Model information, mac address, IP Address, firmware version, program files…etc). This information would then go to a database to track assets. To manually go through each room and either read the device info directly off the device or from the web interface would take an extraordinary effort across a large corporate environment of 200+ conference rooms (or more). Thankfully, Crestron provided us another way: Crestron EDK.

### **Crestron EDK: Crestron Enterprise Development Kit**

![](https://cdn-images-1.medium.com/max/2000/1*TY2crwl1ZVJRbBXvT4EAkg.png)

[Crestron EDK](https://sdkcon78221.crestron.com/sdk/Crestron_EDK_SDK/Content/Topics/EDK-Overview.htm): Crestron Enterprise Development Kit is a *“collection of PowerShell modules that enables users to interface with Crestron devices over Ethernet.” *It comes with an extensive library of commands and arguments that make automating basic tasks like firmware upgrades, and device info gathering a breeze. For example, you can see a sample firmware update script using Crestron EDK. No more manually updating devices one by one. The time /value save by utilizing scripts like these is immense. The future is here, and its automation.

Note: Access to [Crestron EDK](https://sdkcon78221.crestron.com/sdk/Crestron_EDK_SDK/Content/Topics/EDK-Overview.htm) does require a Crestron dealer /technician account.

## Crestron EDK: Installation

The installation is extremely simple. Just follow the steps in the EDK package

 1. login to your pc as admin

 2. download the [EDK package here](https://sdkcon78221.crestron.com/downloads/EDK/EDKSetup-1.0.5.0.zip) (Requires Crestron Login)

 3. Unzip the package and install the setup.exe

 4. The EDK PS modules will install

 5. You’re ready to start scripting!

## Using Crestron EDK

Scripting with EDK does take some getting used to, but thankfully there is an [API reference guide](https://sdkcon78221.crestron.com/sdk/Crestron_EDK_SDK/Content/Topics/PSCrestron.htm#Get-CrestronSession) that Crestron provides. Additionally, it’s fairly intuitive. I went from basically no knowledge of Powershell or EDK to being decently knowledgable on the subject in a matter a couple of months of tinkering.

![](https://cdn-images-1.medium.com/max/3776/1*t4Thc5JI_JAR4kl6W_81uQ.png)

To get started, simply add*** Import-Module PSCrestron ***to the beginning line of your script. This will call the PS Crestron module that will be used later. NOTE: *Do NOT forget this step. *It is the foundation that the script runs on.

From there you can write a script to do almost whatever you need. For example, Let's write a script that takes screenshots of TSW-1060 (or other TSW model) touch panels.

### 1. Open a Crestron session with the device

    $session = **Open-CrestronSession** -Device $d -secure

* the **-secure **argument uses the Crestron default credentials (you can add *-username -password* for specific passwords as well)

* device **$d** is our IP address of the device

### 2. Grab the hostname from the device (typically containing room name) via the hostname command

    $hostnameResponce = **Invoke-CrestronSession** $session “**hostname**”

* this issues the hostname command within the previously established Crestron session

### 3. We can use regex to filter out the hostname output to just the hostname

    **$deviceHostname** = [regex]::Match($hostnameResponce, “(?<=Host\sName:\s)[\w-]+”).value

### 4. Finally we can initiate the ***screenshot ***command

    $screenshot= **Invoke-CrestronSession** $session “**screenshot $deviceHostname**”

* note that we issue the screenshot command, and then call the **$deviceHostname** variable as the screenshot name

* This will name the screenshot the same as the hostname for easy viewing/identification

### 5. Next we’ll grab the screenshot from the panel via FTP

    **$Remotefile** = ('logs\' + **$deviceHostname** + '.bmp')

    **Get-FTPFile** -Device $d -RemoteFile $Remotefile -LocalPath $local -secure

* **$Remotefile** is the storage location of the screenshot on the device. **$Remotefile **concatenates the file path + the hostname (screenshot name) + the .bmp file extension

* **Get-FTPFile** grabs the FTP file from the device (**$d**)

* Lastly **-LocalPath $local**, tells the script we want to save the screenshot in the same LocalPath (listed in the variable **$local**)

* So to recap, this stage of the script grabs the screenshot file via FTP from the device storage and saves it in the same location that the script was run from under the filename of the hostname previously gathered.

### 6. Screenshot Cleanup

    **Remove-FTPFile** -device $d -RemoteFile **$Remotefile** -secure

* **Remove-FTPFile** is a command that deletes a file from the device via FTP

* **$RemoteFile** is the file previously listed in the above step

* Effectively this “leaves no trace” of any screenshot so you don’t have multiple screenshots piling up unnecessarily taking up device storage space

### 7. Close Crestron Session

    **Close-CrestronSession** $session

* this closes the Crestron session

* It is best to close any unneeded sessions when finished

There are other parts of the code that I didn’t mention as I didn’t want to bore the life out of you, however, when finished it should effectively look like [this](https://github.com/AnthonyTippy/Crestron-EDK-Superscripts/blob/main/Screengrabber.ps1). Full script available on [my GitHub](https://github.com/AnthonyTippy/Crestron-EDK-Superscripts/).

![](https://cdn-images-1.medium.com/max/2000/1*gclnOPYaPR_1xpC6eYDQUA.png)

## **Here’s a working screenshot**

* Note: IP’s and other sensitive info has been blurred due to private information.

![](https://cdn-images-1.medium.com/max/2000/1*6gKVzrYNsoCjl2k2lY0IVA.jpeg)

Finally, we have all the screenshots saved to our local script root folder. Now that the script has run, I can easily see with one view that all of the MTR UC-ENGINE codecs that I manage are online and appear to have no visible issues.

![](https://cdn-images-1.medium.com/max/3212/1*skB5woiS-KaLkwPiMvmKBA.jpeg)

With this finished script, we can automate screenshots of touchpanels ranging from Microsoft Teams Room Touchpanels, Room Schedule Panels, Zoom Rooms…etc. I use it nearly daily to remotely check up on many of the high importance rooms on my site. With this script, I don’t have to physically check the room every day/week but can simply run this script on those IP ranges and get a visual status update of every room.

Also, Crestron default Hostnames are typically not changed, so it can be hard to identify what room/system they go to. If you run this script on a Room schedule panel, you can see the schedule for the room, thus telling you what room that IP address correlates to. Then just go in and rename the hostname accordingly.

If you operate or manage a/v devices on a large corporate campus, especially one in which many rooms/buildings can be physically separated, this is a game-changer. Who needs Crestron Fusion Monitoring when you have Powershell?

## Crestron SuperScript

![](https://cdn-images-1.medium.com/max/2000/1*6KJUlvUNb7ZFYaNkG7cihA.jpeg)

Another script I developed to assist with managing Crestron devices is a “[superscript](https://github.com/AnthonyTippy/Crestron-EDK-Superscripts/blob/main/Crestron%20Superscript.ps1)” of sorts. This script gathers a wealth of device information such as MAC address, Ethernet settings, model info, firmware version, and program file loaded (where applicable). Finally, after filtering through every IP address on the IP.txt file it reads from, it outputs all of the info into a CSV file.

It's quite extensive so I won’t post it here due to formatting but feel free to check it out on my [GitHub](https://github.com/AnthonyTippy/Crestron-EDK-Superscripts).

## Here is a sample of the output from the SuperScript

![](https://cdn-images-1.medium.com/max/2720/1*QgrNYla8WZLnD6Ea01Lfyg.jpeg)

If you’ve ever had to do yearly or routine asset/device audits, this can be extremely helpful. Let's say you want to make sure all the control processors or touch panels on your network are up to the latest firmware version? Simply run the script with the IP addresses of your devices, and you can quickly generate a pivot table/chart with the various firmware versions in your network to present to management. From there you can pivot to a PowerShell script that updates all devices listed in the prior report < firmware version 1.2.000 and upgrade them to 2.1.0 (example numbers)

![Here is a sample output of the top 10 firmware versions across multiple devices](https://cdn-images-1.medium.com/max/2142/1*39StPNnTjxItFYnzkxgLxw.png)

## What if I don’t have an IP list?

So what about if you don’t have a pre-existing IP address list to feed into the script? Sure you could manually go around and get the IP addresses but that would take forever, and remember we’re automating to make our life easier.

Luckily there are a couple ways to discover devices in a “brand new to you” network

### 1. Crestron Device Discovery

Crestron device discovery is a feature within [Crestron Toolbox](http://support.crestron.com/app/answers/detail/a_id/32/~/crestron-software---downloading-latest-versions). Chances are if you’re reading this, you probably are very familiar with Crestron Toolbox. If you aren’t, stop reading this and go play with Toolbox. There are far more tools in there than I could ever write up.

Device discovery is effective in finding many Crestron devices, however, it has its limitations. To start, device discovery is limited to the subnet of the host PC so if you have a large segmented network you may have to do multiple scans. Additionally, certain Crestron devices such as the HDMD400 TX/RX, DM-202-TX /RX, and other DM tools are not supported by device discovery.

![](https://cdn-images-1.medium.com/max/2718/0*7vOZxSj2KFwbY4t4.jpg)

### 2. Crestron Info Tool

![](https://cdn-images-1.medium.com/max/2000/1*lk6Dhvi0nOkkZ4BU2GlPUA.png)

The second, and personally; my preferred method of finding new devices, is with the [Crestron Information Gathering Tool](https://www.crestron.com/Products/Control-Hardware-Software/Software/Development-Software/SW-INFOTOOL). InfoTool is a Crestron developed software that is extremely fast and efficient in gathering device information. You can ping specific IP addresses and it will return information such as IP, MAC Address, Serial, TSID…etc. It doesn’t provide as much information as my SuperScript, but it's significantly faster and can serve as a great starting point to pivot from.

One way I’ve recently found to leverage this tool even further is to essentially pivot it into a network-wide Crestron device scanner. InfoTool allows the importing of IP.txt lists in a “batch mode” that it will then scan extremely quickly. So when you pair this with a Powershell script that generates every possible IP address on a subnet/series of subnets, you effectively get a Crestron network-wide device discovery IP scanner. ***Note: **this method is fairly “brute force” in nature, and may trip alerts for security teams. Make sure you give your network security team a heads up before doing this or you may get some “whatcha doing emails”*

With this IP list generator script, it will generate a text document with all IP addresses along with a specific subnet (such as 192.168.1.1–192.168.1.254, or even 192.168.1.1–192.168.5.254), resulting in a massive list of IP addresses to have InfoTool try.

![[https://github.com/AnthonyTippy/Crestron-EDK-Superscripts/blob/main/IP%20List%20Generator.ps1](https://github.com/AnthonyTippy/Crestron-EDK-Superscripts/blob/main/IP%20List%20Generator.ps1)](https://cdn-images-1.medium.com/max/2000/1*uY7iakxKdqGGQXcHvRzKfQ.png)

The [IP List Generator](https://github.com/AnthonyTippy/Crestron-EDK-Superscripts/blob/main/IP%20List%20Generator.ps1) script prompts for the IP address octets ranges desired and generates this list. Info Tool will import your IP list, and begin pinging/scanning every IP address for Crestron devices.

It will return a grid output of all devices it finds, wherein you can save the results to a .csv file. With this method, I’ve found devices that can be more evasive such as in-wall or ceiling transmitter/receivers that previously I was unaware of.

![](https://cdn-images-1.medium.com/max/2546/1*NGSVV7Yq72WoOZTxuclCLw.png)

***Note: **It is **NOT **recommended to load any more than **40,000 **IP addresses into the info tool unless you have a sufficiently powerful PC.*

Even with a large amount of IP addresses (30,000+), the InfoTool filters through the IP list extremely quickly (30k in under 6 minutes). This is much quicker than any script I’ve written, which would take, exponentially longer.

## Recap

There’s a lot of info that I briefly covered in this post, but the best way to learn it is to try it yourself. Go download the EDK package, and start scripting. Try some of the scripts on devices you manage. The benefits of scripting with EDK are numerous and can make deployment of devices and management of installed devices so much easier.

![](https://cdn-images-1.medium.com/max/2000/0*p0wmO2NZ2FGPvcph.jpg)

Prior to a couple of months ago, I only had light Python experience. In the span of 2 months, I was able to teach myself PowerShell basics and leverage a really great library that has made many of the tasks and obligations of my work *SO* much easier. If you have any questions, feel free to leave a comment and I can try to help.

Stay tuned for more scripts on my Github. I’ll be updating the scripts as often as I can and adding more as I develop them.

Have fun automating friends! Hack the planet

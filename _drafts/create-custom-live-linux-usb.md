---
layout: post
title: Create Custom bootable Live Linux USB
subtitle: How to boot to a customied Linux from USB
published: false
tags: Linux
---

## Use Cubic to create a custom ISO

Whenever I travel and need to use a machine where I need to login with my credentails, I am wary or hesitant to do so. In such cases, I've always carried with myself a bootable USB that boots to a clean Ubuntu OS. That way, I am sure that the environment I enter my credentials on is clean. 

Over time, I found I was running a few tasks repeatedly after booting into the USB. I installed Chrome, ran updates, joined the network, installed one or more tools, customized a thing here and there. Naturally what I next looked to was to see if these common operations could be "baked" into the ISO i.e. create a custom bootable USB drive and that's what this post is about.

To create custom ISO's we use [Cubic](https://launchpad.net/cubic).

## Install Cubic
Install Cubic on an Ubuntu (this is what I had at hand). You can also do the below operations in a VM too. Do note that the source ISO must be within the VM though (not on a shared drive that's networked in). 

Launch Cubic and select a project folder. This is where your ISO changes are tracked. 

![image](https://user-images.githubusercontent.com/327990/65850434-76819180-e381-11e9-92a8-ed360b65640b.png)


Specify the location of the source ISO and folders for target ISO:

![image](https://user-images.githubusercontent.com/327990/65850408-5ce04a00-e381-11e9-9313-473f7f5ec781.png)

Hit Next

![image](https://user-images.githubusercontent.com/327990/65850391-43d79900-e381-11e9-927c-f5f8e5a910c9.png)

We now enter a terminal where we do the "customization" of our ISO. I am customizing the following:
1. Create a bootstrap script in `/usr/bin/local` with 755 permission) that:
	* joins my home Wi-Fi (using `nmcli`)
	* Calls a hosted script that does a bunch of other stuff (listed later below). This is where I keep customized scripts that I can change any time.
2. Install Chrome
3. Install VPN clients
4. Remove unwanted packages 
5. Customize my shell
6. Load my NAS folders (if online)

Use [Rufus](https://rufus.ie/) to burn to USB (bootable USB).

## The bootstrap script
I save this script in `/usr/bin/local` 

```bash
#!/bin/bash
nmcli device wifi connect ssid password 'zxxxxxx'
wget -O- mydomain.com/profile >> ~/.profile
source ~/.profile
wget -O- mydomain.com/scripts | bash
```

The last line calls an externally hosted script that runs whatever is in there. 

{: .box-warning}
**Warning:** Do note the dangers of this - this shouldn't contain any credentials nor publicly accessible. 
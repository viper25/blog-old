---
layout: post
title: Create Custom ISO
subtitle: Each post also has a subtitle
bigimg: /img/path.jpg
published: true
categories: Test
---
{: .box-warning}
**Warning:** TEST POST


## Use Cubic to create a custom ISO

Install Cubic on Ubuntu (the distro I chose) from [here](https://launchpad.net/cubic).

Launch Cubic and select a project folder. This is where your ISO changes are tracked. 

![image](https://user-images.githubusercontent.com/327990/65850434-76819180-e381-11e9-92a8-ed360b65640b.png)


Specify the location of the source ISO and folders for target ISO:

![image](https://user-images.githubusercontent.com/327990/65850408-5ce04a00-e381-11e9-9313-473f7f5ec781.png)

Hit Next

![image](https://user-images.githubusercontent.com/327990/65850391-43d79900-e381-11e9-927c-f5f8e5a910c9.png)

We now enter a terminal where we do the "customization" of our ISO. I am customizing the following:
1. Join my home Wi-Fi (by running a script on boot)
2. Install Chrome
3. Remove unwanted packages 
4. Cutomize my shell


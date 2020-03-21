---
layout: post
title: Create Custom bootable Live Linux USB
subtitle: How to boot to a customied Linux from USB
published: true
tags: Linux
---


## Use Cubic to create a custom ISO

Whenever I travel and need to use a machine where I need to login with my credentails, I am wary or hesitant to do so. In such cases, I've always carried with myself a bootable USB that boots to a clean Ubuntu OS. That way, I am sure that the environment I enter my credentials on is clean. 

Over time, I found I was running a few tasks repeatedly after booting into the USB. I installed Chrome, ran updates, joined the network, installed one or more tools, customized a thing here and there. Naturally what I next looked to was to see if these common operations could be "baked" into the ISO i.e. create a custom bootable USB drive and that's what this post is about.

To create custom ISO's we use [Cubic](https://launchpad.net/cubic).

## Install Cubic
Install Cubic on an Ubuntu (this is what I had at hand). You can also do the below operations in a VM too. Do note that the source ISO must be within the VM though (not on a shared drive that's networked in). 

If you get an error such as:
```
The following packages have unmet dependencies:
 cubic : Depends: xorriso (>= 1.3.2) but it is not installable
         Recommends: isolinux (>= 3:6.03) but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
```
Select the "community maintained and software restricted by copyright options in "Software Sources". Run `sudo apt update` and try again.

![](https://i.stack.imgur.com/cGmRz.png)

## Launch Cubic
Launch Cubic and select a project folder. This is where your ISO changes are tracked. 

![image](https://user-images.githubusercontent.com/327990/65850434-76819180-e381-11e9-92a8-ed360b65640b.png)


Specify the location of the source ISO and folders for target ISO:

![image](https://user-images.githubusercontent.com/327990/65850408-5ce04a00-e381-11e9-9313-473f7f5ec781.png)

Hit Next

![image](https://user-images.githubusercontent.com/327990/65850391-43d79900-e381-11e9-927c-f5f8e5a910c9.png)

## Customize the ISO
We now enter a terminal where we do the "customization" of our ISO. We are presented with a terminal where we can customize the ISO image:

![image](https://user-images.githubusercontent.com/327990/74652427-f9847680-51c0-11ea-816f-a948f167d6f7.png)

 (It's best to save these actions as a script in a [gist](https://gist.github.com/)) in case you need to recreate the ISO.

### Create a Bootstrap script

First, create a bootstrap script named say `vjk-boot.sh` in `/usr/local/bin` with 755 permission). This is to be run manually (or on startup of the ISO) to do the following:
	* joins my home Wi-Fi (using `nmcli`)
	* Calls a hosted script that does a bunch of other stuff (listed later below). This is where I keep customized scripts that I can change any time. An example of this bootstrap script would be:
	
```bash
#!/bin/bash
nmcli device wifi connect mywifi_ssid password 'wifi_password'
wget -O- profile.example.com >> ~/.profile
source ~/.profile
wget -O- boot.example.com | bash
```

The last line calls an externally hosted script (on boot.example.com) that runs whatever is in there. 

{: .box-warning}
**Warning:** Do note the dangers of this - this shouldn't contain any credentials nor publicly accessible. 

The ISO image can be customized 	with additional settings that needn't be in the bootstrap script (things that take time to setup, such as installing Chrome, VPN clients etc.)

### Install latest OS updates 
`sudo apt update && sudo apt upgrade`

### Install Chrome
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
### Install VPN clients
```bash
mkdir /opt/OpenVPN/Windscribe_OpenVPN
```
Copy the `.ovpn` files and `auth-user-pass.txt` in this directory. Place the certs `ca.crt` and `ta.key` in a sub folder named `openvpn_cert`.

### Install rclone
A very useful tool when using Custom Linux ISOs is to use the [mount](https://rclone.org/commands/rclone_mount/) feature of rclone to mount cloud drives such as Google Drive, OneDrive, Box etc.

[Install](https://rclone.org/downloads/) rclone and then [configure](https://rclone.org/commands/rclone_config/)  to get tokens for the cloud drive of your choice. Then [mount](https://rclone.org/commands/rclone_mount/) and enjoy! 

Do note, when configuring in the Cubic terminal, the tokens for the cloud drives are stored at `~/.config/rclone/`. Move this to your home folder for the target user (i.e. `ubuntu`); the current terminal in Cubic is root and will not be where rclone looks for the config when using the Custom ISO. Hence move it to `/home/ubuntu/.config`

Create a helper script at `/usr/local/bin/` named say, `touch mount_cloud.sh` that will have the mount command: 
```bash
rclone mount box:linux_mount /mnt/cloudrive/box
```
When needed to mount just run `sudo mount_cloud.sh`

### Remove unwanted packages 
```bash
sudo apt-get remove --purge libreoffice*
sudo apt-get purge thunderbird*
sudo rm /usr/share/applications/ubuntu-amazon-default.desktop
```
### Customize my shell

## Add or Remove packages
In the next screen select and/or remove packages that are not needed:
![image](https://user-images.githubusercontent.com/327990/74652853-eaea8f00-51c1-11ea-9262-35a7807d0b4f.png)

Click Generate when done.
![image](https://user-images.githubusercontent.com/327990/74653716-b7106900-51c3-11ea-86f8-e6c1b65f1b7a.png)

## Generate ISO & Delete the project
The final screen does allow you to delete all project files (minus the generated disk image). If this is deleted, you cannot continue customizing this ISO. You can you the newly created Custom ISO as the starting point for the next custom ISO and create a new project folder.
 
![image](https://user-images.githubusercontent.com/327990/74657031-5c2e4000-51ca-11ea-8ac7-318851a23c35.png)

Burn the generated ISO (in the Custom folder) using  [Rufus](https://rufus.ie/) to an USB to make a bootable USB. 

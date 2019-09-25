---
layout: post
title: Add Signal notifications to Synology NAS
subtitle: Get alerts
published: true
tags: technology
---

So, I want to be alerted of activities to my phone when say, my NAS boots up or when a backup is complete. We try to do this using the [signal-cli API](https://github.com/AsamK/signal-cli).

# Setup Signal on Synology NAS
First order of business is to install Java (`signal-cli` needs Java to work). Now download `signal-cli`  to any folder on the NAS. You can download this on your PC from the [releases](https://github.com/AsamK/signal-cli/releases) section and place it on any of your shared folders.

![image](https://user-images.githubusercontent.com/32394146/32131412-1276de22-bbe0-11e7-9a9f-0b94c7fa8463.png)

Or you could so this by SSH into the NAS. First enable SSH in Synology:

![image](https://user-images.githubusercontent.com/32394146/32131422-334c855c-bbe0-11e7-8ed7-f4366075894c.png)

Then ssh in as:

```bash
ssh admin@nas
```

Navigate to a folder you want to download signal-cli to

```bash
cd /volume2/downloads/signal-cli-0.5.6
```

Follow the instructions at the Repo's [home page](https://github.com/AsamK/signal-cli).

```bash
export VERSION=<latest version, format "x.y.z">
sudo wget https://github.com/AsamK/signal-cli/releases/download/v"${VERSION}"/signal-cli-"${VERSION}".tar.gz
sudo tar xf signal-cli-"${VERSION}".tar.gz -C .
```

Now add a symlink to `usr/local/bin` which is in the `PATH` so that signal-cli can be accessed from any location.

```bash
sudo ln -sf /volume2/downloads/signal-cli-"${VERSION}"/bin/signal-cli /usr/local/bin/
```

Now test if you can call the API by registering your number (as the SENDER).

```bash
sudo signal-cli -u <your_phone_number> register
```

Follow the registraton and verification process as described in the repo's [Usage section](https://github.com/AsamK/signal-cli#usage).

{: .box-warning}
**Warning:** It isn't instantaneous. Took a minute or two for the registration and verification commands to complete. You might think something's wrong, but just wait a minute or two.

Test send a message from the command line:

```bash
signal-cli -u <your_phone_number> send -m "Completed backup up on $day at $hostname" <recipient_number>
```

Now you can call `signal-cli` from any script in NAS. Let's take a look at onedrive

# Send Signal Notification from Synology

Under Task Scheduler, create a user defined script and at the end, add the Signal Notification message. Here's an example where I have my NAS update my IP address to afraid.org, the free Dynamic DNS. 

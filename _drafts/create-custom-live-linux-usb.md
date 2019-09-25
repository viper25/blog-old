---
layout: post
title: Create Custom bootable Live Linux USB
subtitle: How to boot to a customied Linux from USB
published: false
tags: Linux
---

Whenever I travel and need to use a machine where I need to login with my credentails, I am wary or hesitant to do so. In such cases, I've always carried with myself a bootable USB that boots to a clean Ubuntu OS. That way, I am sure that the environment I enter my credentials on is clean. 

Over time, I found I was running a few tasks repeatedly after booting into the USB. I installed Chrome, ran updates, joined the network, installed one or more tools, customized a thing here and there. Naturally what I next looked to was to see if I could create a custom bootable USB drive and that's what this post is about.

# Cubic	

I came upon [Cubic](https://launchpad.net/cubic) that is a "GUI wizard to create a customized bootable Ubuntu Live CD (ISO) image". 

Add the Cubic repo and install per instructions:

```bash
sudo apt-add-repository ppa:cubic-wizard/release
sudo apt update
sudo apt install cubic
```


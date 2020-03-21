---
layout: post
title: Install Jekyll on Ubuntu
subtitle: Install on Ubuntu Live USB/CD
published: true
tags: Linux, Jekyll
---

There's quite a lot of info on how to install Jekyll on Ubuntu and most don't work. Here's how to install [Jekyll](https://jekyllrb.com/) on an Ubuntu Live USB.


## Use Cubic to create a custom ISO

Adapted from [here](https://computingforgeeks.com/how-to-install-jekyll-on-ubuntu-18-04/).

Update the system

```bash
sudo apt update
sudo apt -y upgrade
sudo reboot
```

Install Ruby development tools

```bash
sudo apt -y install make build-essential
sudo apt -y install ruby ruby-dev
```


We now need to instruct Ruby’s gem package manager to place gems in logged in user’s home directory. Add below line to ~/.bashrc or ~/.zshrc depending on your shell,

```bash
export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
```

```bash
sudo gem install bundler
sudo gem install jekyll
```

Udpate Bundler
```bash
sudo bundle update --bundler
```

Done! Jekyll installed. 


Build your site and make it available on a local server

```bash
bundle exec jekyll serve
```

Browse to http://localhost:4000

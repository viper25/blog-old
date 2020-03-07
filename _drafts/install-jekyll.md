---
layout: post
title: Install Jekyll on Ubuntu
subtitle: Install on Ubuntu Live USB/CD
published: false
tags: Linux
---


## Use Cubic to create a custom ISO

Follow Instructions [here](https://computingforgeeks.com/how-to-install-jekyll-on-ubuntu-18-04/).

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
gem install bundler
gem install jekyll
```

Udpate Bundler
```bash
bundle update --bundler
```

Done! Jekyll installed. 


Build your site and make it available on a local server

```bash
bundle exec jekyll serve
```

Browse to http://localhost:4000

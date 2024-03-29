---
layout: post
title: Install Jekyll on Ubuntu
subtitle: Install on Ubuntu Live USB/CD
published: true
tags: Linux, Jekyll
---

There's quite a lot of info on how to install Jekyll on Ubuntu and most don't work. Here's how to install [Jekyll](https://jekyllrb.com/) on an Ubuntu Live USB.

This was tested on an Amazon EC2 running Ubuntu. Once SSH'd into the system:

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

Update Bundler

Navigate to the root directory of the Jekyll site (that contains the `Gemfile`) and run:


```bash
sudo gem install bundler
sudo gem install jekyll
sudo bundle update --bundler
```

{: .box-error}
For some Jekyll sites, if you get an error such as 
`An error occurred while installing nokogiri (1.10.10), and Bundler cannot continue.
Make sure that ``gem install nokogiri -v '1.10.10' --source 'https://rubygems.org/'`` succeeds before bundling.`, run `sudo apt-get install build-essential patch ruby-dev zlib1g-dev liblzma-dev`



Done! Jekyll installed. Build your site and make it available on a local server:

```bash
bundle exec jekyll serve
```

Browse to http://localhost:4000

To server over an EC2 (for testing), run as 
```bash
bundle exec jekyll serve --host=0.0.0.0
```
---
layout: post
title: Setup Jekyll on Windows
subtitle: Run popular static site generator in Windows
published: true
tags: technology
---

Jekyll is a blog-aware, static site generator. It is built for Linux and Mac OS and not guaranteed to work on Windows or officially supported. I've followed [this](http://jekyll-windows.juthilo.com/) link to setup Jekyll on Windows 10, but added some more detail and excluded some others in this post. Here's how you set it up.


## Install Ruby & configure

Get Ruby from the Ruby [download page](https://rubyinstaller.org/downloads/). I couldn't get my setup working using Ruby 2.4.2-2 (x64), so I had to revert to Ruby 2.3.3 (x64). I prefer to use portable versions wherever I can, so I chose to download the [7-zip archive](https://dl.bintray.com/oneclick/rubyinstaller/ruby-2.3.3-x64-mingw32.7z). Also download [Ruby Development kit](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe).

It's best to create a folder with no space and install (or unzip) to it. I used `C:\RUBY`.

![image](https://user-images.githubusercontent.com/327990/31006103-eefd40bc-a52d-11e7-91ee-bea3aaebb373.png)

I also hesitate of permanently add folders to my Windows PATH environment variable, so I create a bacth file that I execute before I do a Jekyll session. It's a simple file that just needs to contain the path to the needed executables. Create a file called, say `env2.3.3.bat` that contains the following: 

```
SET PATH=%PATH%;C:\RUBY\RubyDevKit\bin;C:\RUBY\ruby-2.3.3-x64-mingw32\bin
```

Run it before proceeding. Run this each time you want to run Jekyll. Next, initialize the DevKit and bind it to your Ruby installation. Navigate to the `C:\RUBY\RubyDevKit` folder and run

```
ruby dk.rb init
```

This will generate a file `config.yml` in this folder. Open this file and add the path to the Ruby installation. Note to change the slashes to a forward slash.

![image](https://user-images.githubusercontent.com/327990/31006247-85836fac-a52e-11e7-963f-be5f21f6c0a6.png)

Install the DevKit, binding it to your Ruby installation.

```
ruby dk.rb install
```

## Install Gems

Ruby has a package manager called [Gems](http://guides.rubygems.org/what-is-a-gem/). We use this to install the Jekyll and [bundler](http://gembundler.com/) gems:

```
gem install jekyll
gem install bundler
```

If you are using GitHub pages to host your site, you need to make sure the Jekyll plugins you use are supported by GitHub Pages. Verify this at [GitHub Pages gem](https://github.com/github/pages-gem). Refer to the relevant [GitHub](https://help.github.com/articles/configuring-jekyll/) page on this too.



{: .box-warning}
**On Use with Github Pages Gem:** The Github Pages gem ignores all plugins included in the Gemfile. If you only include a plugin say, `jekyll-sitemap` in the Gemfile without also including it in the `_config.yml` the plugin will not work. This can be confusing because the official Jekyll docs state that plugins can be included in either the Gemfile or `_config.yml`.


## Build the site

Get a Jekyll site from say, [Jekyll Themes](http://jekyllthemes.org/themes/jekflix/). In a commnd prompt, go to the folder of the site you just downloaded. It ought to look something like this:

![image](https://user-images.githubusercontent.com/327990/31006731-896b557e-a530-11e7-832e-2390d3fb09bb.png)

Run:

```
bundle exec jekyll serve
```

If you see the message below:

![image](https://user-images.githubusercontent.com/327990/31006776-c537317c-a530-11e7-9902-339d97fd8b9b.png)

Run the command as requested

```
bundle install
```

Once it's completed, run:

```
bundle exec jekyll serve
```
![2017-09-29_16-14-40](https://user-images.githubusercontent.com/327990/31006926-5649ec72-a531-11e7-9cde-867d473547af.gif)

Navigate to the URL shown and you should see the static site:

![image](https://user-images.githubusercontent.com/327990/31007020-a22774de-a531-11e7-85a5-96586294edc4.png)

You can update your bundle & gems once a while using

```
gem update
```

or if Bundler is installed, run

```
bundle update
```

And that's it! 

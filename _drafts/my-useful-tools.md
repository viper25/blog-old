---
layout: post
title: Tools!
subtitle: A list of tools I find most useful
published: true
categories: Test
permalink: /tools/
---


Over the years we all collect tools and install favourites that make them indespensible when setting up a new PC. So this page will be a continuously updated page that has MY tools both for the Windows and Linux (Ubuntu) platofrms. All tools listed below are free, where it isn't, I'll explicitly say so.

# Windows

*  [FileZilla](https://filezilla-project.org/download.php?type=client): the best FTP client out there. No hassles. The best part is the update process - I do not have to re-provide my configration settings each time I do an update (like Notepad++ does).

*  [7-ZIP](http://www.7-zip.org/download.html) - No nonsense zip/unzip tool that integrates with the shell. I never give any programs a presence in my shell except for 7-Zip. Useful since you'd need to right-click and zip/unzip many a time.

*  [Notepad++](https://notepad-plus-plus.org/download/): The Text editor of choice. Light-weight and extensible with useful plugings and themes (I don't care about themes much, but for those who do, it's there). 

*  [rclone](https://rclone.org/) : Not the greatest backup tool, it is buggy (with IO errors when syncing with the cloud), but until I find a good, free alternative, I'll use this.

*  [Grsync](https://sourceforge.net/projects/grsync/files/latest/download): For when you need to use rsync on Windows. Unfortunately It's hosted on SourceForge (which has known to be shady in bundling unwanted software with downloads). 

* [Bvckup](https://bvckup2.com/): The best, simplest Windows differential backup tool. It's paid software, but worth the $ you pay for it. At $19.95 it's a steal. 

*  [ShareX](https://getsharex.com/): Hands down the best screengrab utility. I was using SnagIt until I happened upon this one. It's free, [open-source](https://github.com/ShareX/ShareX/) and has tons of features. Almost anything you can do with alternative commercial software, you can do with ShareX.

*  [Paping](https://code.google.com/archive/p/paping/): Simple equivalent of telnet for systems that do not have telnet. I use this to test if ports are open from any machine. Also available for Linux

## Chrome Extensions

*  OneTab
    
	
#Linux

*  Handy commands to add to you .profile

```bash
alias ll='ls -lrhtF --group-directories-first'
alias off="sudo shutdown -h now"
alias cls='clear'
alias cd..="cd .."
#list our disk usage in human-readable units including filesystem type, and print a total at the bottom:
alias df="df -Thah --total"
alias free="free -mth"
alias grep="grep --color=auto"
 
#Grep History
alias histg="history | grep"
 
#Make a dir and change to it
function mkcd {
	mkdir -p "$1" && cd "$1"
}
 
#Transfer files using transfer.sh website
transfer() { if [ $# -eq 0 ]; then echo "No arguments specified. Usage:\necho transfer /tmp/test.md\ncat /tmp/test.md | transfer test.md"; return 1; fi
tmpfile=$( mktemp -t transferXXX ); if tty -s; then basefile=$(basename "$1" | sed -e 's/[^a-zA-Z0-9._-]/-/g'); curl --progress-bar --upload-file "$1" "https://transfer.sh/$basefile" >> $tmpfile; else curl --progress-bar --upload-file "-" "https://transfer.sh/$1" >> $tmpfile ; fi; cat $tmpfile; rm -f $tmpfile; }
```
	
*  [bmon](https://github.com/tgraf/bmon): Monitor bandwidth

*  [seashells](https://seashells.io/): Mirror an interactive shell. A great tool and something that ought to be built into the standard Linux terminal. If you have a long running job or wish to view your terminal remotely, use this. Amazing tool!

# Firefox Plugins

*  Lastpass
*  uBlock Origin
*  Change this setting: `about:config --> browser.sessionstore.interval = 60,000`
*  cliget


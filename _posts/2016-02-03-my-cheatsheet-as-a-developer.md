---
title: "My cheatsheet as a developer"
layout: post
cover: false
categories: 'blog'
tags: 'blog dev'
comments: true
navigation: True
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-03 11:52:43 EST
---

This will be a summary about tools, commands, useful links that help me in my day to day life. And it will be kept updating..

## Cheatsheets

- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)

## Transimission common commands

- [TransmissionHowTo](https://help.ubuntu.com/community/TransmissionHowTo)

And the location of the settings.json => /etc/transmission-daemon/settings.json

**Note:**

Make sure you stop the daemon first before you make any modification to the setting file.

```
#restart transimission-daemon
service transmission-daemon start
service transmission-daemon stop
service transmission-daemon restart
```

## Useful resources for Web Developers
[IE Test VMs](https://dev.windows.com/en-us/microsoft-edge/tools/vms/)
Download them using curl:

```
# IE7 - Vista
curl -O "https://az412801.vo.msecnd.net/vhd/VMBuild_20141027/VirtualBox/IE7/Windows/IE7.Vista.For.Windows.VirtualBox.zip"

# IE8 - XP
curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/IE8_XP/IE8.XP.For.MacVirtualBox.ova"

# IE9 - Win7
curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/IE9_Win7/IE9.Win7.For.MacVirtualBox.part{1.sfx,2.rar,3.rar,4.rar,5.rar}"

# IE10 - Win8
curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/IE10_Win8/IE10.Win8.For.MacVirtualBox.part{1.sfx,2.rar,3.rar}"

# IE11 - Win8
curl -O "https://az412801.vo.msecnd.net/vhd/VMBuild_20141027/VirtualBox/IE11/Windows/IE11.Win7.For.Windows.VirtualBox.zip"

# Edge - Win10
curl -O "https://az792536.vo.msecnd.net/vms/VMBuild_20150801/VirtualBox/MSEdge/Windows/Microsoft%20Edge.Win10.For.Windows.VirtualBox.zip"
```

**Tips** To extract a sfx file:

```
chmod +x abc.sfx
./abc.sfx
```

### Vagrant boxes from MOdern.ie

Official links can be found [modernIE on hashicorp.com](https://atlas.hashicorp.com/modernIE/)

- XP with IE6: http://aka.ms/vagrant-xp-ie6
- XP with IE8: http://aka.ms/vagrant-xp-ie8
- Vista with IE7: http://aka.ms/vagrant-vista-ie7
- Windows 7 with IE8: http://aka.ms/vagrant-win7-ie8
- Windows 7 with IE9: http://aka.ms/vagrant-win7-ie9
- Windows 7 with IE10: http://aka.ms/vagrant-win7-ie10
- Windows 7 with IE11: http://aka.ms/vagrant-win7-ie11
- Windows 8 with IE10: http://aka.ms/vagrant-win8-ie10
- Windows 8.1 with IE11: http://aka.ms/vagrant-win81-ie11

**To import a vagrant box file:**

```
$ vagrant box add {title} {url} # vagrant box add win7ie11 win7ie11.box
$ vagrant init {title} # vagrant init win7ue11
$ vagrant up
```

### Vagrant file to provison the modernIE vm

- Refer to this link in github - [Setup modern.ie vagrant boxes](https://gist.github.com/andreptb/57e388df5e881937e62a)
- And this blog is also very helpful - [ModernIE Vagrant Boxes](https://joecod.es/modernie-vagrant-boxes/)

__Note__ credit belongs to [bram.us](https://www.bram.us/2014/09/24/modern-ie-vagrant-boxes/)

__User name and Password:__

  - username = "IEUser"
  - password = "Passw0rd!"



## Setup your mac with brew and brew cask

brew and brew cask are really really nice tool for a developer to automate the installation and configuration of your mac environment. 

There are many articles talking about how to do this. This link is helpful as a start: [Setup Mac OS X](https://gist.github.com/cstipkovic/9118447)



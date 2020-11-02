---
title: "Setup your Macbook as a developer machine"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-07-18 10:48:26 EDT
---

Create this article to summarize my scirpts to setup my Macbook:

## Install ruby and rvm

```bash
curl -sSL https://get.rvm.io | bash -s stable --ruby
# install bundler
gem install bundler
# Add the following line into .bash_profile or .zshrc
source ~/.rvm/scripts/rvm
```

## Setup VIM

```bash
brew rm vim vim python
brew install python
brew install vim --with-override-system-vi
```

#### Note: if python3 is not installed or configured as default

```bash
brew install macvim --with-cscope --with-lua --with-override-system-vim --with-luajit --with-python
brew linkapps macvim
```

#### Troubleshooting

Sometimes you get weird errors in VIM, due to the integration of various libraries.

One error you might frequently see in MacVim is about python:

```bash
E887: Sorry, this command is disabled, the Python's site module could not be loaded.
```

Follow this [link](http://www.oschrenk.com/vim-youcompleteme-and-python/) regarding how to install vim properly in Mac.

**Note:**
Sometimes you will have to reinstall everything to resolve this.




## Intellij-IDEA

```bash
brew cask install intellij-idea-ce
```

## iTerm configuration

### Setup zsh/oh-my-zsh

```bash
# install zsh first
brew install zsh zsh-completions
# install oh-my-zsh on top of zsh
curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
#make zsh the default shell if not yet
chsh -s /usr/local/bin/zsh
```

#### Configure iTerm color thems

> Download and configure [iTerm color thems](https://github.com/mbadolato/iTerm2-Color-Schemes)

#### configure zsh themes


```bash
# Add the following into .zshrc
ZSH_THEME=pygmalion

# enable plugins for git, vagrant, etc.
plugins=(git vi-mode colored-man colorize github vagrant brew mvn Forklift gradle httpie node npm pip python ruby rvm screen tmux osx zsh-syntax-highlighting)
```

**Note:** if you receive the following errors when using fl for [Forklift](http://www.binarynights.com/forklift/), it's very likely caused by the assistive access for Script Editor.

> System Events got an error: osascript is not allowed assistive access. (-1719)

To enalbe the assitive access, go to **System Preferences > Security & Privacy > Privacy > Accessibility.**

![Assitive Access](/assets/images/assistive_access.png)

Make sure **Script Editor** is checked in the list.

### Configure SSH with remote server

- [How To Configure SSH Key-Based Authentication on a Linux Server](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

## enable vi mode in zsh

```bash
export VISUAL=vim
autoload edit-command-line; zle -N edit-command-line
bindkey -M vicmd v edit-command-line
```

# ssh-config

## store passphrase to keychain

Add you key file to keychain

```bash
/usr/bin/ssh-add -K /path/to/private_key
```

**Note** make sure use the capital `K`, and if it complains about the option not supported, make sure you use `/usr/bin/ssh-add`.

in your `~/.ssh/config` file

```bash
 Host server.example.com
    IdentityFile ~/.ssh/id_rsa
    UseKeychain yes
```

If you are sharing your ssh configuration with systems running older versions of OpenSSH that don't understand the UseKeychain option, you can specify the IgnoreUnknown option to keep your configuration compatible with both new and old versions, like this(just put it at the beginning of the config file):

```bash
IgnoreUnknown UseKeychain
```

See details in https://developer.apple.com/library/archive/technotes/tn2449/_index.html
And also https://github.com/jirsbek/SSH-keys-in-macOS-Sierra-keychain

## Configure Rime input (For Chinese text input)

- [安装及配置 Mac 上的 Rime 输入法——鼠鬚管 (Squirrel)](https://www.dreamxu.com/install-config-squirrel/)

## Troubleshooting

- I have recently experienced a random issue that iTerm hangs and I have to do a OS reboot to clear it up. It's fairly painful, since Terminal.app is affected also. I ended up using [Hyper Terminal](https://hyper.is/) as a backup when this occurs and I don't want to reboot. I haven't figured out the root cause of the issue yet. Here is a [stackover flow discussion around the same issue](http://apple.stackexchange.com/questions/267668/terminal-login-hangs/269286). I will post an update once I have this fixed.
- Use `time zsh -c -i exit` to tune up the zsh loading time.

### Tune startup time for zsh

If you notice slow startup time of zsh, you can use the following command to measure the startup time. And then you can adjust the zsh config to see how you can optimize it. A binary search is usually very helpful to identify what's caused the slowness. Somehow, I found `nvm` is incredibly slow on MacOS. So I have to create a function to only enable it when I need it.

```bash
time zsh -i -c exit
```

- Another option is to use `zprof` to find out what has contributed to the longer loading time.
- If you can also use lazy load for some time-consuming plugins to reduce the startup time. Refer to this article: - https://kevin.burke.dev/kevin/profiling-zsh-startup-time/

## Reference

- [My Mac OS X development setup](http://www.codejuggle.dj/my-mac-os-x-development-setup/)
- [Install Ruby on Rails 5.0 · Mac OS X El Capitan](http://railsapps.github.io/installrubyonrails-mac.html)
- [Awesome MacOS command line](https://github.com/herrbischoff/awesome-macos-command-line/blob/master/README.md#ssh)
- [tune the zsh loading performance](https://htr3n.github.io/2018/07/faster-zsh/)

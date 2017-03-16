---
title: "Setup your Macbook as a developer machine"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
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

![Assitive Access](/images/assistive_access.png)

Make sure **Script Editor** is checked in the list.

#### Troubleshooting

- I have recently experienced a random issue that iTerm hangs and I have to do a OS reboot to clear it up. It's fairly painful, since Terminal.app is affected also. I ended up using [Hyper Terminal](https://hyper.is/) as a backup when this occurs and I don't want to reboot. I haven't figured out the root cause of the issue yet. Here is a [stackover flow discussion around the same issue](http://apple.stackexchange.com/questions/267668/terminal-login-hangs/269286). I will post an update once I have this fixed.


## Reference

- [My Mac OS X development setup](http://www.codejuggle.dj/my-mac-os-x-development-setup/)
- [Install Ruby on Rails 5.0 · Mac OS X El Capitan](http://railsapps.github.io/installrubyonrails-mac.html)

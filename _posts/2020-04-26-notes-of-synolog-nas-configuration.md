---
title: "Notes of Synolog NAS configuration"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-04-26 13:12:09 EDT
---

## Setup package manager

[Entware](https://github.com/Entware/Entware/wiki/Install-on-Synology-NAS) is the recommended package manager on Synology NAS. And [this link](https://www.eigenbahn.com/2020/04/29/synology-entware) actually uses an ansible script to automate the installation, which I should actually try!

use this script to determine the architecture of the NAS:

```bash
\
printf "\nProcessor:   "; \
cat /proc/cpuinfo | \
grep "model name" | \
grep "[^:]*$" -o  | \
uniq; \
printf "Architecture: "; \
uname -m; \
printf "\n"
```

## Setup ssh login

What's tricky is really the permissions you need to change:

```bash
admin@syno$ chmod700 .ssh
admin@syno$ chmod 644 .ssh/authorized_keys
admin@syno$ chmod 755 /var/services/homes/admin
```

- refer to: [SSH without password on Synology DSM6.x](http://www.cesareriva.com/ssh-without-password-on-synology-dsm6-x/)

## Setup Git Server

It's easy to install the git server using package center. What could be tricky is to setup the user access:

- create a user named as `git` from control panel.
- grant git access in the git server (by opening the git server from installed packages in package center)
- also make sure a user folder is created for the `git` user, which can be done in `Control Panel` -> `Users` -> `Advanced` -> `Enable user home service`
- ssh to the synology server and create a `git-shell-commands` folder under  `~git`, e.g. `mkdir ~git/git-shell-commands`
- If a custom ssh port is used, you need to use the following git command to specify the ssh port:
  - `git clone ssh://git@mydomain.com:[port]/gitrepo`

**Note** I have run into issues related to the ssh access for the `git` user. And I find using the `admin` user seems the easiest to do (though definitely not a best practice to do, especially not feasible if there are multiple users)

### Refer: [Setting Up a Git Server On a Network Access Storage (NAS)](https://medium.com/future-vision/setting-up-a-git-server-on-a-network-access-storage-nas-ce1505228521)

## Enable Rsync

By default, `rsync` is not enabled in synology DSM. To turn it on, navigate to `Control Panel` -> `File Station` -> `rsync`

More details can be found in the following link:

- [Strange rsync error on Synology DSM](https://www.going-flying.com/blog/strange-rsync-error-on-synology-dsm.html)

---
title: "setup a docker environment using vagrant"
layout: post
cover: false
categories: 'blog'
tags: 'blog devops'
navigation: True

comments: true
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-01-31 10:45:03 EST
---

I have played with docker a little bit about one or two years ago, when it began popular everywhere. However, since I don't really need to use it for my work at that time. I didn't spent a lot of time on it. 

Very recently, some of our development and test environment have been moved to docker now. So it's time to think about how could I setup a docker environment on my macbook easily.

I did some research before I started. [Vagrant](https://www.vagrantup.com/) was the first one came up. I have used it before. It is really convenient and easy to provision a vm by define/configure a vagrant configuration file, including docker. So you won't need to waste your time to install the image, configure the server. Isn't it nice!

I am using this article to summarize something helpful I found during the use of vagrant and docker:

## Vagrant file I use:
This is the vagrant file I use right now. It gives me a docker environment provisioned, and has a local folder mapped to the virtual machine, and also has a network port(80) mapped to the host machine(10080).

```ruby
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.provision "docker"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.network :forwarded_port, host: 10080, guest: 80
end
```



## Find the host ip address
Sometime it is not very straightforward to figure out the accessible host ip address from inside the vm. The following command will help you. 
** Note **  Credit belong to [stackoverflow](www.stackoverflow.com)

```bash
# Get the host ip that can be used from inside of the guest os.
netstat -rn | grep "^0.0.0.0 " | cut -d " " -f10
```


---
title: "use nginx and vagrant to configure a reverse proxy server"
layout: post
cover: false
categories: 'blog nginx devops'
tags: 'blog vagrant devops'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-10-12 21:47:50 EDT
---

For some reasons, macOS doesn't allow you to run applications on the default http or https port. But sometimes you might want to have your application run on the default port. To achieve it, you can actually leverage a virtual vm and configure a reverse proxy using nginx.

Thanks to the vagrant and its auto-provisioning function, it's actually quite easy to create a vagrant box with everything configured.

### First, you need to configure a vagrant box which will have nginx installed:

```bash
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
  # use bootstrap.sh script to do the initial setup
  config.vm.provision :shell, path: "bootstrap.sh"

  # configure private network(i.e. host-only network, so the vm can be accessed using the specified ip)
  config.vm.network "private_network", ip: "192.168.33.10"

  # map the data folder to the /vagrant folder inside the vm, so you can place the nginx site setting 
  # file (i.e. default) and ssl certifacte inside the folder, therefore it can be accessed from the 
  # mapped folder.
  config.vm.synced_folder "./data", "/vagrant", type:'nfs'
end
```

### Then we look at what need in the bootstrap.sh

```bash
#!/usr/bin/env bash
# update the OS
apt-get update
# install nginx
apt-get install -y nginx
# use the site setting in data folder to overwirte the default one
cp /vagrant/default /etc/nginx/sites-enabled/
# start the server after everything is done
service nginx start
```

### At last, look at what need to be configured for nginx as a reverse proxy

Let's look at what we need to have in the default nginx setting file

```bash
upstream proxied.localhost {
    server 192.168.33.1:9443;
}
server {
    listen 443 ssl default_server;
    server_name    _; # Catch all, see http://nginx.org/en/docs/http/server_names.html

    server_name gusproxy;
    # make sure the ssl certificate is in place, skip this if you only run the proxy for http
    ssl_certificate /vagrant/ssl/ca.pem;
    ssl_certificate_key /vagrant/ssl/ca.key;

    ssl_protocols               TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers   on;

    # used cloudflares ciphers https://github.com/cloudflare/sslconfig/blob/master/conf
    ssl_ciphers                 EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5;

    # config to enable HSTS(HTTP Strict Transport Security) https://developer.mozilla.org/en-US/docs/Security/HTTP_Strict_Transport_Security
    # to avoid ssl stripping https://en.wikipedia.org/wiki/SSL_stripping#SSL_stripping  
    add_header Strict-Transport-Security "max-age=31536000; includeSubdomains;";

    server_tokens off;

    add_header X-Frame-Options SAMEORIGIN;

    add_header X-Content-Type-Options nosniff;

    client_max_body_size 50M;

    location /mypath {
	# change to whatever host/port the docker container is listening on.
        proxy_pass https://proxied.localhost/galaxy; 
        # set the Host as the original Host the users see
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_read_timeout 3m;
        proxy_send_timeout 3m;
    }
}
```

## Summary

When you have all of the above in place, it is so easy to launch it as a reverse proxy:

```bash
# start the vm, it will start the provisioning process automatically the first time, i.e. copy files, install nginx, etc.
vagrant up

# after the server is up, you can use vagrant ssh to get inside the vm
vagrant ssh

# when you want to shutdown the vm, exit it, and run vagrant halt
vagrant halt
```


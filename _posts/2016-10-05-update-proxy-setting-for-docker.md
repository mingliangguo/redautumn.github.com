---
title: "Update proxy setting for docker"
layout: single
categories: 'blog docker'
tags: 'blog docker'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-10-05 20:54:15 EDT
---

This might not be common, but we have to work with proxy to access our docker server, to set a proxy, you can add the following in your .bashrc:

```bash
export HTTP_PROXY=${your_http_proxy_server}
export HTTPS_PROXY=${your_https_proxy_server}
```

With this being set, I am able to access the docker registry without problems. However, what drove me crazy is that they changed the ip address of the proxy. And I thought it was quite straightforward, that after I changed the proxy setting, it should just work! However, how naive I was! After I made the change to point to the new proxy server, and try to pull new image, I was receiving an error complaining about not able to access the proxy, the OLD one!! So I checked everywhere that I could think of, .bashrc, .bash_profile, /etc/profile, ... none of them has the old settings.

After some search in Google, I found the [http proxy configuration document](https://docs.docker.com/engine/admin/systemd/#http-proxy) from docker website. 

So actually docker will create a http.conf file to store the http proxy configuration. 
> The article asked user to create it, but I believe docker will also create it itself if it's not created.

The setting is in the following file => **/etc/systemd/system/docker.service.d/http-proxy.conf** 

```bash
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:80/"
```

If you open the file, you find the old proxy setting is just there. So what you need to do is to update the setting to point to the new proxy server.

And after that, make sure you reload the setting and restart docker daemon:

```bash
# flush the settings
$ sudo systemctl daemon-reload

#Verify that the configuration has been loaded:
$ systemctl show --property=Environment docker
> Environment=HTTP_PROXY=http://proxy.example.com:80/

# restart docker daemon
$ sudo systemctl restart docker
```

That's it!

## References:

- [HTTP-PROXY Control and configure Docker with systemd](https://docs.docker.com/engine/admin/systemd/#http-proxy)
- [Running Docker behind a proxy](https://crondev.com/running-docker-behind-proxy/)






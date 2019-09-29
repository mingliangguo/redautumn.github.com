---
title: "Cheatsheet for Httpie"
layout: single
categories: 'blog programmer web'
tags: 'blog web http'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-10-03 12:49:27 EDT
---

[Httpie](https://httpie.org/) is a fantastic command line tool that help you do more http interations using the command prompt, similar to curl, but much much better.

## Make http GET with authorization header
```
http -v https://api.box.com/2.0/files/12345678 'Authorization:Bearer <access_token>'
```

### Download top 50 songs from Netease Music

- Credit from [Sutra Zhou](https://feedly.com/i/entry/CdO4oMiqEuoiHIBRXUch+5nrnT1jzSOd/3CkEd5fU4c=_15b15c3cfae:34ecf76:5d3506ae)

```bash
curl 'http://music.163.com/artist?id=973004' \
| pup 'ul.f-hide a json{}' \
| jshon -a -e href \
| awk -F\t '{system("you-get \"http://music.163.com/"$1"\"")}'
```

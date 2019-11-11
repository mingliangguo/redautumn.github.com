---
title: "Cheatsheet for IBM Cloud"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-11-07 22:23:06 EST
---


```bash
# login to ibmcloud cli
ibmcloud login --apikey <path_to_the_api_key_file>
# list all clusters
ibmcloud ks cluster ls
# list resource groups
ibmcloud resource groups
ibmcloud target -g <resource_group_name>
# connect to a specific cluster
ic ks cluster config --cluster <cluster_name>
```

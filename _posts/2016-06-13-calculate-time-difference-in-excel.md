---
title: "Calculate time difference in Excel"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-06-13 12:05:33 EDT
---

I need to analyze some logs produced in our application, which involves a lot of time calculation. And I think Excel is a good tool to help me calculate the time difference and then I can also use it to visualize the time duration.

However, it is not as easy as I expected. It did take me some time to figure out how to calculate time differences with a timestamp. 

Basically by default Excel only allows you to represent time in seconds, not milliseconds. To calculate the time difference, you first need to define a custom time format which has milliseconds, i.e. `[h]:mm:ss.000`. And then second is the separator between second and millisecond has to be '.', not ':'!!

After that, you can simply use `=TEXT((C2-B2), "h:mm:ss.000")` to calculate the difference! 

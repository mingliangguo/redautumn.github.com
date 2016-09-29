---
title: "Third-party cookies and P3P"
layout: post
cover: false
categories: 'blog web security'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-06-29 09:17:01 EDT
---

This is to keep a note about some cookie related problems I recently ran into. It's pretty much IE related.. 

## 3rd-party cookies

So what is 3rd-party cookies? It is not as implied by the name, cookies from a different domains, which is for sure to be prevented by the browser. A definition from [Mozilla](https://support.mozilla.org/en-US/kb/disable-third-party-cookies):

> Third-party cookies are cookies that are set by a website other than the one you are currently on. For example, cnn.com might have a Facebook like button on their site. That like button will set a cookie that can be read by Facebook. That would be considered a third-party cookie.

As described above, a 3rd-party cookie typically happens when a website is indirectly accessed by the users. The indirect access could be links referred by the main website, or a website included in an iframe. The iframe scenario is a most popular situation that developers will run into. And for security consideration, most browsers provide option/settings to allow user to turn on/off the third-party cookie. And IE 11(and lower), plus Safari have disabled 3rd-party cookie by default. Chrome, Firefox and Edge allow it by default, but provide option to disable it.

## What we can do if 3rd-party cookies is disabled?

Based on the summary above, if you know your web application is going to be embedded by other website, you should try to avoid relying on cookies, so you don't need to deal with the 3rd-party cookie problem. 

But sometimes you may not always have a choice, or sometimes it's too late to know that you run into this pitfall (that's what we met). And it's good that we finally got an agreement on not using iframe. How lucky we are!! 

If you have to deal with the 3rd-party cookie limitation, there is a standard called [Platform for Privacy Preferences Project (P3P)](https://en.wikipedia.org/wiki/P3P) which is supposed to allow website to declare their intent on using the cookie. However the protocol/standard is not well receieved by the major browsers. IE has some level of support of it. I have tried using fiddler to set the p3p header and it does help to bypass the 3rd-party constraints. But I haven't tried it with Chrome and other browsers, whether it works or not when 3rd-party cookies are disabled. I haven't seen anyone in the internet who claimed to use P3P to solve the 3rd-party cookies problem. 

## Some articles I think are helpful to understand the 3rd-party cookie and P3P

- [A Quick Look at P3P](https://blogs.msdn.microsoft.com/ieinternals/2013/09/17/a-quick-look-at-p3p/)
- [P3P, Cookies and IE6.0: A Case Study](https://www.sitepoint.com/p3p-cookies-ie6/2/)
- [3rd-party cookies in practice](https://blog.zok.pw/web/2015/10/21/3rd-party-cookies-in-practice/)
- [Third-Party Cookies vs First-Party Cookies](http://www.opentracker.net/article/third-party-cookies-vs-first-party-cookies)
- [Third party cookies with IE at 2am](http://labs.fundbox.com/third-party-cookies-with-ie-at-2am/)
- [How to disable third-party cookies in all major web browsers](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers)
- [Policy Generators and Implementation Tools](http://www.p3ptoolbox.org/tools/resources1.shtml)o

## Bonus - Another fun fact of Internet Explorer

This one might be something good. :-) At least, it follows the requirement of a real standard. It's basically about handling illegal characeters in DNS names. Read the following article for details.

- [Why Internet Explorer Won’t Allow Cookies On (sub)domains With Underscores](https://ma.ttias.be/internet-explorer-wont-allow-cookies-subdomains-underscores/)



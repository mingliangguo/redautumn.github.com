---
title: "Jacoco plugin in Jenkins"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2018-09-18 15:08:33 EDT
---

Jacoco has been used in the project to assure the test coverage. However, I didn't realize that the jacoco job in jenkins is using a different plugin than the one setup in our source code repository. 

One thing got my attention was the test coverage failure in our pipeline for one of the service we work on. And it's a surprise because the coverage has been pretty good in the past and suddenly failed in a PR with small changes. By digging into the log, I realized that the coverage report in the pipeline has included the test code itself!! And it's interesting to see that the coverage of the test code is not 100%!! Guess that's because of the test framework code and some of the tests are only enabled/used for some flags. But anyway, that's a separate topic.

So once you know the root cause of the issue, then it's just a matter of finding the right person to help you fix it! Since it worked before, it's apparently caused by some recent changes in the pipeline. And one thing we found during the investigation is that the exclusion rules of the jacoco plugin doesn't work as expected. i.e. it won't exclude the test code as it's supposed to do. We have to make sure the source we specify only contains the source code not the test code (which is where the problem came in.). The [discussion here](https://stackoverflow.com/questions/42265838/how-to-have-code-coverage-in-jenkins-with-jacoco-and-multiple-modules) has an example of the right way to configure the plugin in jenkins. Instead of configuring the exclusion rules, it works better to make sure the `Path to source directories` only contain the source code.

If you are using [Lombok](https://projectlombok.org/) in your project, another thing worthy to note is that the latest version of jacoco and lobmok allow you to ingore the lombok generated code in the coverage report. Here is one article - [Ignoring Lombok Code in Jacoco](https://www.rainerhahnekamp.com/en/ignoring-lombok-code-in-jacoco/) with some of the details. Just be aware that you would need the latest version of jacoco plugin for jenkins if jenkins is used in the pipeline.

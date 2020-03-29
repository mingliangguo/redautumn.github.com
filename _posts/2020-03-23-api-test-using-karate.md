---
title: "API Test using Karate"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-03-23 10:24:56 EDT
---

API test is very important for microservice development. You need a test suite that continuously tests your service and validate it works as expected. Or any new changes are not causing regressions.

For my own experience, I have been with projects using different API test tools:
- [Gatling](https://gatling.io)
- [artillery]*(https://artillery.io)

However both Gatling and artillery focus more on performance testing rather than functional testing. And for Gatling, as it's written in scala, which is not a super popular language and has a relatively high learning curve. And artillery, on the opposite, is written in node, and the test scripts can be expressed in yaml, which is very nice. However, when the scenario becomes compplex, and you need to verify some relative complex data, it is hard to do. And also, sharing the reusable code in yaml is also a challenge.

Then I run across [karate](https://github.com/intuit/karate), which is very nice API testing framework. It's created for API testing and uses the BDD style DSL to write the test scripts. One part I like particularly is the documentation of karate. The developers of Karate have done a fantastic job of documenting everything about the framework.


## Troubleshooting

#### Debug in VS code
Karate has very good documentation and has pretty debugging support in VS Code. The [tutorial](https://github.com/intuit/karate/wiki/IDE-Support#vs-code-karate-plugin) in the website is very easy to follow.
However, I did run into one issue during debug configuration in VS code. Basically, when I set a breakpoint and launch the debugger, as soon as it hit the breakpoint, the debug hangs with an error like this:

```
java.lang.NoSuchFieldError: toStringWriter
        at com.intuit.karate.JsonUtils$NashornObjectJsonWriter.writeJSONString(JsonUtils.java:80)
```

After spending some time for troubleshooting, it looks like somehow the dependency of the JsonWriter wasnot loaded properly, to bypass this error, you can explicitly load the dependency:

```groovy
  testCompile "net.minidev:json-smart:2.3"
```

## References

- [Top 10 Most Popular API Testing Tools](https://medium.com/@CapitalTerefe/top-10-most-popular-api-testing-tools-62c43eefb870)
- [Karate API Testing Tool Cheat Sheet](https://www.testingexcellence.com/karate-api-testing-tool-cheat-sheet/)
- [11 top open-source API testing tools: What your team needs to know](https://techbeacon.com/app-dev-testing/11-top-open-source-api-testing-tools-what-your-team-needs-know)

---
title: "Gradle Cheatsheet"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-09-23 12:30:45 EDT
---

Try to summarize some common command for gradle:

## Run a specific test case 

```bash
./gradlew test --tests "abc.test.XyzTest"
```

## Generate the default folder structure

```bash
# for Java project
gradle init --type java-library

# The default java-library project has the following features enabled:
# Uses the “java” plugin
# Uses the “jcenter” dependency repository
# Uses JUnit for testing
# Has directories in the conventional locations for source code
# Contains a sample class and unit test, if there are no existing source or test files

# more options for java project
gradle init --type java-library --test-framework spock: Uses Spock for testing instead of JUnit

# for scala project
gradle init --type scala-library

gradle init --type java-library --test-framework testng: Uses TestNG for testing instead of JUnit

# for groovy project
gradle init --type groovy-library

# for basic setup
gradle init --type basic
```

- [Reference - gradle build init plugin](https://docs.gradle.org/current/userguide/build_init_plugin.html)

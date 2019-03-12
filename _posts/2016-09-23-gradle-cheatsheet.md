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
## Run a specific class

Basically you can use `JavaExec` task to achieve this, for example, you can add an `execute` task in your build.gradle file:

```bash
task execute(type:JavaExec) {
   main = mainClass
   classpath = sourceSets.main.runtimeClasspath
}
```

To run a sepcific class, 

```bash
gradle -PmainClass=Foo.Bar execute
```

> Note: `mainClass` is the name of class you want to run and passed in at command line.

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

## show dependencies for your gradle project

```bash
gradle dependencies
gradle htmlDependencyReport
## for sub-projects
gradle sub-project-name:dependencies
gradle sub-project-name:htmlDependencyReport
```

or if you want to show the dependencies for all of your sub-projects, add the following into your top level `build.gradle`

```groovy
subprojects {
    task listAllDependencies(type: DependencyReportTask) {}
}
```

## Lock dependencies

You can use dynamic dependency versions and still lock them to specific versions with the Gradle Dependency Lock Plugin](https://plugins.gradle.org/plugin/nebula.dependency-lock) from Netflix’s Nebula Plugins project.

```bash
gradle generateLock saveLock
```


- [Reference - understand gradle dependencies](https://www.devsbedevin.com/android-understanding-gradle-dependencies-and-resolving-conflicts/)
- [Locking Dependency Versions in Gradle](https://jkutner.github.io/2017/03/29/locking-gradle-dependencies.html)

## Use artifact from a local project

Sometimes you might want to use an artifact from a local project where you may have some local changes that haven't been pushed to the artifactory yet. Suppose you have two project (A, B), and you want to use a local build from project B in project A.

To do so, you need to:

### In both project

Make sure you have `maven` plugin added, and also have `mavenLocal` in your repository setting.

```groovy
apply plugin: 'maven'
buildscript {
    repositories {
        mavenLocal()
        maven {
        // your official artifactory config
        }
    }
    ...
}

```

> Note, if you have sub-projects for each project, make sure the above is applied to all sub-projects.

### In Project B

Use `gradle publishToMavenLocal` to publish the build artifact to your local maven repository. Once it's done, you should be able to find the build artifact in your local maven repository `${user.home}/.m2/reposistories`.

## exclude test and/or check

```
gradle clean build -x check -x test
```

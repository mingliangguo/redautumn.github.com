---
title: "Import gradle project into eclipse"
layout: single
categories: 'blog'
tags: 'blog tech eclipse gradle'
navigation: True
comments: true
subclass: 'post tag-speeches'
date: 2016-02-11 10:36:24 EST
---

I have to work with some projects that are created using [gradle](http://gradle.org/). And when I tried to import the project into eclipse, I had run into issues and it took me quite some time to figure it out.

First, there are several different eclipse plugins that allow you to work with Gradel. At first, I used [Gradle Integration for Eclipse](https://marketplace.eclipse.org/content/gradle-integration-eclipse-0). But I always got a 'null error' in the eclipse UI and an error like this *Could not fetch model of type 'HierarchicalEclipseProject' using Gradle distribution* in the eclipse log file.

And in the log under the .metadata folder you probably could see something like the following:

```
java.lang.reflect.InvocationTargetException
	at org.springsource.ide.eclipse.gradle.core.util.GradleRunnable.run(GradleRunnable.java:112)
	at org.eclipse.jface.operation.ModalContext$ModalContextThread.run(ModalContext.java:119)
Caused by: org.eclipse.core.runtime.CoreException: Could not fetch model of type 'HierarchicalEclipseProject' using Gradle distribution 'https://services.gradle.org/distributions/gradle-2.0-bin.zip'.
	at org.springsource.ide.eclipse.gradle.core.util.ExceptionUtil.coreException(ExceptionUtil.java:40)
	at org.springsource.ide.eclipse.gradle.core.util.GradleRunnable.run(GradleRunnable.java:104)
	... 1 more
Caused by: org.gradle.tooling.GradleConnectionException: Could not fetch model of type 'HierarchicalEclipseProject' using Gradle distribution 'https://services.gradle.org/distributions/gradle-2.0-bin.zip'.
	at org.gradle.tooling.internal.consumer.ResultHandlerAdapter.onFailure(ResultHandlerAdapter.java:59)
	at org.gradle.tooling.internal.consumer.async.DefaultAsyncConsumerActionExecutor$1$1.run(DefaultAsyncConsumerActionExecutor.java:57)
	at org.springsource.ide.eclipse.gradle.core.modelmanager.GradleProjectModelManager.getModelInternal(GradleProjectModelManager.java:141)
	... 6 more
Caused by: org.gradle.api.artifacts.ResolveException: Could not resolve all dependencies for configuration ':testRuntime'.
    ...
Caused by: java.lang.RuntimeException: Problems reading data from Binary store in /private/var/folders/14/c5cqz92j17z1nvz6hg3tynp40000gn/T/gradle105063885390697438.bin (exist: true)
	at org.gradle.api.internal.artifacts.ivyservice.resolveengine.store.DefaultBinaryStore$SimpleBinaryData.read(DefaultBinaryStore.java:126)
	... 68 more
Caused by: java.lang.NullPointerException
	at org.gradle.api.internal.artifacts.ivyservice.resolveengine.result.DefaultResolutionResultBuilder.resolvedConfiguration(DefaultResolutionResultBuilder.java:61)
	at org.gradle.api.internal.artifacts.ivyservice.resolveengine.result.StreamingResolutionResultBuilder$RootFactory.deserialize(StreamingResolutionResultBuilder.java:184)

```

I tried various suggestions I found in Google, stackoverlow. e.g.

- Using JDK7
- Delete the /private/var/folders/14
- Using the gradle in my system instead of the one in the wrapper.
- Recreate a new eclipse project, and re-import
- Switch to a different gradle plugin [Gradle Eclipse IDE by BuildShip](http://gradle.org/eclipse/), which is the official one suggested by Gradle.

Unfortunately, none of them work.

At last, I tried to specify the latest version for gradle using the [Gradle Eclipse IDE by BuildShip](http://gradle.org/eclipse/) plugin. And this time, it works!!! So it seems that the error I have been seeing is really related to the version of gradle. It needs the latest version to make the import work. The version used in the wrapper is not new enough. It is really frustrating to spend so much time to figure this out.

![Configure the gradle version](/assets/images/gradle_import.png)



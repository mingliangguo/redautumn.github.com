---
title: "Mockito Cheatsheet"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2018-07-16 09:46:57 EDT
---


As a Java developer, Mockito is your good friend for unit test. Using this to record some frequently used Mockito usages:

## Verify if a method is called or not called.

```java
Mockito.verify(mockObject, times(5)).mockMethodToVerify(); // verify a method is called 5 times.
Mockito.verify(mockObject, never()).mockMethodToVerify(); // verify a method is never called.
```

## Control the behavior of a mocked method based on the passed in parameters

```java
when(someMock.someMethod()).thenAnswer(new Answer() {
    private int count = 0;
    public Object answer(InvocationOnMock invocation) {
        if (count++ == 1)
            return 1;
        return 2;
    }
});
```

## Use captor to capture function arguments

```java
ArgumentCaptor<HashSet> captor = ArgumentCaptor.forClass(HashSet.class);
verify(obj).update(anyString(), captor.capture());
assertEquals("the captured HashSet should be empty.", 0, captor.getValue().size());
```
## Use answer to return the parameter passed into a method.

```java
when(mock.someMethod(anyString())).thenAnswer(invocation -> invocation.getArguments()[0]);
```

Or more simpler, using the built-in method by `Mockito` - [AdditionalAnswers](https://static.javadoc.io/org.mockito/mockito-core/2.2.7/org/mockito/AdditionalAnswers.html).

```java
  when(mock.someMetod(anyString(), anyString()))
      .thenAnswer(AdditionalAnswers.returnsFirstArg());
  when(mock.someMetod(anyString(), anyString()))
      .thenAnswer(AdditionalAnswers.returnsSecondArg());
  when(mock.someMetod(anyString(), anyString()))
      .thenAnswer(AdditionalAnswers.returnsArgAt(2));
```

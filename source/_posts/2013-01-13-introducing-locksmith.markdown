---
layout: post
title: "Introducing Locksmith"
date: 2013-01-14
comments: true
categories: [.NET, Locksmith]
hidden: true
---
## What if you could mock (almost) anything in .NET?
### Introducing Locksmith for the .NET framework

Mocking libraries have dramatically simplified the process of unit testing dependency injected code. But although a number of good mocking libraries exist for the .NET framework, they are handicapped in a way that their counterparts in Java are not. Most mocking libraries work by dynamically generating a subclass of the type being mocked, and overriding its methods to return values (or take other actions) as specified in the test. However, in .NET most methods are not virtual and cannot be overridden. This [policy](http://www.artima.com/intv/nonvirtual.html) of [non-virtual](http://www.artima.com/forums/flat.jsp?forum=106&thread=14374) by [default](http://neverindoubtnet.blogspot.com/2009/08/do-not-make-every-method-virtual.html) has been [hotly](http://ayende.com/blog/4126/virtually-everything) [debated](http://programmers.stackexchange.com/questions/144574/should-all-public-methods-in-an-abstract-class-be-marked-virtual), and will undoubtedly continue to be debated for some time to come. But with Locksmith, this policy doesn't keep you from mocking dependencies in your test code.

Locksmith lets you treat all visible instance methods and properties in all loaded assemblies as virtual. That means that you can use your favorite mocking library to mock what is normally a non-virtual method, and it will just work. And it doesn't just work on your own code; non-virtual methods in other libraries, including the BCL, can be mocked with Locksmith. A single method call before any of your test code is executed is all that is required. For example, if you are using NUnit as your testing framework:

``` c# Using Locksmith with NUnit (C#) https://bitbucket.org/eatdrinksleepcode/locksmith/wiki/Using%20EagerKey%20with%20NUnit Wiki Page
[SetUpFixture]
public class SetUpFixture {

    [SetUp]
    public void SetUp() {
        new EagerKey().UnlockReferences();
    }
}
```

To get started using Locksmith, visit the [project page](https://bitbucket.org/eatdrinksleepcode/locksmith).
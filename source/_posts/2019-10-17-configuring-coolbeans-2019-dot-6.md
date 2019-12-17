---
layout: post
title: "Configuring CoolBeans 2019.6"
date: 2019-10-17 22:29
comments: true
categories: java NetBeans CoolBeans OpenBeans maven
---

> Now CoolBeans has been renamed OpenBeans

At JDK 8, JavaFX and the JDK were together, thus already configured to build applications with both.  Since that time, they were split apart (by Oracle). Different groups took over the open-source versions of each (JDK, JavaFX, and the IDE).  Each of these components needed work, which was done on different schedules, so at this point, one has to do a bit of work to set up CoolBeans (or NetBeans) for JavaFx work.  Additionally, it has become apparent that developers need to ship the JVM with their products to reduce the pain to their users.

This [Gist][] discusses the approach as well as provides the files used.

The approach features

* use of modular Java
* latest JavaFX
* integration with CoolBeans (Run, Debug, Generate JavaDoc, Test with TestNG)
* an image that contains everything (for the platform it was built on) to run the program

Testing is configured but not demoed.

[Gist]: https://gist.github.com/dgreen/e1ae4636f311d38758dafdd7b0decf0f

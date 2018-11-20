---
layout: post
title: "Finding Java and NetBeans"
date: 2018-11-19 23:01
comments: true
categories: java, NetBeans
---

Working with NetBeans 9 with an OpenJDK 10 install on a MacOS Mojave machine.

I teach a course EE333 where we use Java as the basis for our efforts in learning object-oriented design and programming.  We had to migrate to NetBeans 9 as NetBeans 8.2 became unworkable in some environments and unsupported.  We also went to Java 10.  First with Oracle although on November 16, 2018 they started wanting to uninstall it and have users move to Java 11 which I gather is going to have long-term support.

Both the Oracle code and the OpenJDK code for MacOS have a new (to me at least) structure where it has a more Mac-like file structure with a "Contents" folder in between the JDK-name and the "Home" directory.  There is also a MacOS folder and an info.plist.

![/Library/Java Directory with JDK 10 on MacOS](/images/jdk10-dir-layout.png)

This means that the `JAVA_HOME` should be set a bit differently (to `/Library/Java/JavaVirtualMachines/jdk-10.0.2.jdk/Contents/Home`) in the ~/.bash_profile configuration file.

There were several errors in the Ant-based building in NetBeans 9 which essentially were stating that it was not possible to find the `java` executable and that the RT (runtime) version would be used instead.

In the build.xml file (on lines 120, 121, 127, 362, and 378 on the file I had), there was a path error that may either be just an error or more likely something that is not built correctly for the later JDK versions.  This removed a bunch of error messages.  

An example (120, 121) of this in diff form (leading spaces removed) is

```diff
-  <available file="${java.home}${file.separator}${file.separator}bin${file.separator}java"/>
-  <available file="${java.home}${file.separator}${file.separator}bin${file.separator}java.exe"/>
+  <available file="${java.home}${file.separator}..${file.separator}bin${file.separator}java"/>
+  <available file="${java.home}${file.separator}..${file.separator}bin${file.separator}java.exe"/>

```

But then, it looks like on restart, NetBeans did not like it and in nbproject/UPDATED.TXT it says

```plain 
============================================
Project ScheduleBuilder build script updated
============================================

Project build script file jfx-impl.xml in nbproject sub-directory has not been recognized
as compliant with this version of NetBeans JavaFX support module. To ensure correct
and complete functionality within this NetBeans installation the script file has been
backed up to jfx-impl_backup.xml and then updated to the currently supported state.

FX Project build script auto-update may be triggered on project open either after
NetBeans installation update or by manual changes in jfx-impl.xml. Please note that
changing jfx-impl.xml manually is not recommended. Any build customization code should
be placed only in build.xml in project root directory.

Remark: The auto-update mechanism can be disabled by setting property
javafx.disable.autoupdate=true
Automatic opening of this notification when project files are updated can be disabled by setting property
javafx.disable.autoupdate.notification=true
(in build.properties, private.properties or project.properties).

Remark: Files nbproject/jfx-impl_backup*.xml and this file nbproject/UPDATED.TXT
are not used when building the project and can be freely deleted.
```

which essentially undid the changes.  Good news is that the error messages are not (yet) back.  I removed
the two files noted as removable.

I will try to remember to check the NetBeans 10vc3 to see if the issue still exists.

In the JDK11, JavaFX will be removed from the JDK and become a standalone package to maintain and install.  Both NetBeans and Java are on multi-times a year release cycle making it challenging to keep up with things for a class baseline.  Hopefully, a stability point is soon.  I know many folks are working towards this goal.



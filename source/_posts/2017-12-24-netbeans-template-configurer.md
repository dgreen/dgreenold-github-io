---
layout: post
title: "NetBeans Template Configurer"
date: 2017-12-24 23:07
comments: true
categories: 
---

Many years ago, I wrote a [post][oldpost] about how to use the NetBeans template system for
my students.  It quickly covered the basics and demonstrated how to set things up
for the course's documentation standard.

In Fall 2017, one of the *UAB EE333* Project teams built a clever tool to do
this initialization for the student.  This makes it much easier for the new
student to set up the automation at the beginning before they have any real
experience with  NetBeans.  The tool solicits the data needed (student name,
email, course) and installs the templates.

It has been tested on both *Windows 10* and *Mac OS 10.12* with *NetBeans 8.2* and attempts
to work with earlier and later versions of things but that is mostly outside the
testing space.  The team consisting of

* Dylan Dalton
* Schauber Gbalou
* Matthew Manuel
* Joey Richardson
* Darrin Wang

have agreed to having the source code of their tool on GitHub under a MIT
license.  UAB students should be able to find a compiled version of the code
in the form of a `templates.jar` file in their course Learning Management
System.

The students cleverly put the basic templates (modified versions of the ones in 
NetBeans) in the jar file as resources allowing one to modify the templates as desired but only have to distribute a jar file to new students.

[oldpost]: blog/2009/09/24/configuring-netbeans-to-produce-custom-documentation-header/

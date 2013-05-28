---
layout: post
title: Determining Version of JVM used to build class file
tags: 
---
The details are given in [Thiam Teck's Blog][1].

Basically, the command

    javap -verbose ClassName

is given and the extensive dump is mined for the major version and minor
version of java used. The cited blog gives a table of major/minor pairs that
go from 1.0 through 1.6.

Another way (if you have binary dump program) is to look at the first 8 bytes
of the .class file as discussed in [Real's How To][2]. For my [example
file][3], the first bytes are:

    CA FE BA BE 00 03 00 2D

The first four bytes `CA FE BA BE` are a signature for a .CLASS file, while
the next two bytes are the minor version (3) and the major version (2D or 45
base 10). The cited article (and the JVM documentation) will match this up to
JVM 1.1 for the example file. Version 1.5 of the JVM runs this class file with
no problem.  Real's How To also gives a sample program for those who have a
binary editor.

[1]: http://thiamteck.blogspot.com/2007/11/determine-java-class-file-version.html
[2]: http://www.rgagnon.com/javadetails/java-0544.html
[3]: http://www-ece.eng.uab.edu/DGreen/java_ex/SimpleClient/SClient0.class

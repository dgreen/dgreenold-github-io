---
layout: post
title: Old code on new platforms
tags: 
---
OS X made the jump to a 64bit platform with 10.6 Snow Leopard.  Of course, not
everything is written for 64 bit mode at present.  The Universal file format
allows for binaries to be containers hold many different copies of the same
code but for different architectures.

So specifically, I was trying to build the latest **rcov** for the platform to
run under the now creaky old Locomotive shell I have been modifying to keep my
development rails environments separate from the OS's installation.  Dutifully
giving the command while inside a terminal session where the paths map to
locations within the Locomotive container:

`gem install rcov`

was giving the right "words" for output including the fact that the binary
extensions were being built (although it happened really quickly!).  Looking
inside, I found the rcovrt.bundle that was built and verified it was being
copied into position.

But using

`file rcovrt.bundle`

I found that it was a `Mach-O x86_64` rather than like the other bundles that
were already there that were `Mach-O i386` bundles.

I found the `Makefile` for the rcovrt code and tried it.

`make clean

> make<br> make install`

Based on hints from [Mac OS X Snow Leopard + Rails, MySQL, and Sphinx][1], I
added

`-arch i386`

to all `CFLAGS`, `CXXFLAGS`, `LDFLAGS`, `LDSHARED` variables, redid the
"`make` dance".  Success, I had the right type bundle in the right place and
everything was working again.

[1]: http://blog.d27n.com/2009/08/26/mac-os-x-snow-leopard-rails-mysql-and-sphinx/


---
layout: post
title: "Adding to a non-privileged users path in Windows 7"
date: 2013-06-05 15:35
comments: true
categories: Windows7
---

Does it have to be this hard?

Anyway, if you are looking for how to add to a non-privileged user's
search path for command line usage, the command `setx` is what you are 
looking for.  While it can be used to modify the system search path, users
don't have permission to do that in many enterprise deployments.
The paths specified by the user are at the end of the system paths.

To see the existing path

        echo %path%

        C:\Ruby193\bin;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\

To put C:\Users\dgreen\bin on the path, use

        setx path C:\Users\dgreen\bin

Once you start a new CMD session, you can see the impact of your changes.

        echo %path%

        C:\Ruby193\bin;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;c:\Users\dgreen\bin

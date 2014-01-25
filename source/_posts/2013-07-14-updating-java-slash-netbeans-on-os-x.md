---
layout: post
title: "Updating Java/NetBeans on OS X"
date: 2013-07-14 17:41
comments: true
categories: java, developer
---
## Oracle Java on OS X##

After moving to Oracle's Java to use on OS X, one finds a new System
Preference pane which launches a Java preferences App.  Included here is a
preset option to update Java.  However, one should note that if one installed
the JDK (Java Development Kit) as opposed to the JRE (Java Run Time
environment) **only** the JRE portion of the package is automatically updated.
It appears one has to manually download and update the JDK to get that portion
of the package updated.  Investigating a bit, it  looks like the attention is
on the JRE and only the linkages for the Applet usage are updated
automatically.  The JDK and its command line version of java are not updated
in addition to all the other components of the JDK.  This is probably not all
bad as it means the development environment does not change on you without
notice.

## NetBeans on OS X ##

To update NetBeans, download a later version, start the new version and agree
to migration from  the earlier release.  Then, when you are ready to eliminate
the old version of NetBeans, go to the /Applications/NetBeans directory and
delete only that old version.

Update:  25 Jan 2014 -- The template directory is made when the first
template is created.  On the Mac, it is located at `~/Library/Application\ Support/NetBeans/7.4/config/Templates`
and has a `Classes` directory and a `Properties` directory.  It appears that one can move the templates
from one config directory to a new one as part of migrating.

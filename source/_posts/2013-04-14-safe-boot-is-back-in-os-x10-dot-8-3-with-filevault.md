---
layout: post
title: "Safe Boot is back (in OS X10.8.3) with FileVault"
date: 2013-04-14 02:01
comments: true
categories: 
---
Safe booting for FileVault users is now possible again in OS X 10.8.3.  As always, you hold down the (left) shift key right after the chime when booting.  You are next taken to the unlock/login screen where you must authenticate by one of the accounts that will unlock the disk.  I hold the shift key down right after the "return" key is hit.  Then you will see the gray progress bar implying booting in safe mode.  After a while (probably after the fschk and other things are done but the progress bar only makes it about 40% across), it will go to the spinner for a while, then just the Apple, and then back to the unlock/login screen but you will notice a red "<span style="color:red">Safe Boot</span>" in the upper right hand corner.  After logging in again, one gets to the operating level of Safe Boot.  You will notice (as always) that your "start at login" items won't be loading -- one of the features of Safe Boot. 

On my old Mac Mini, things are pretty slow in Safe Boot.  It  must be disk intensive as my SSD-based MacBook Pro is much faster.

Since safe boot is the safe way to fix some things like

    Sandboxd: ... mdworker(..) deny mach-lookup com.apple.ls.boxd

It is great to have this working again.

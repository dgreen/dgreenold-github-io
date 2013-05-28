---
layout: post
title: Snow Leopard - smooth install
tags: 
---
![Snow Leopard][1]I have now installed Snow Leopard on 3 machines (1 more to
go plus a server).

I had waited about a week and between the effort the vendors put in before the
release and the updates that came out a bit later, only a few issues arose
during the upgrade process.

I am able to use the built-in CISCO VPN support and after I fixed the
[keychain access issue][2], I did not have to supply my password every
connection.  I also learned that one can use CMD+SHIFT+G to change a browse
window to another directory including the ones that are not easily browsable
by the Apple GUI.

I'll talk about conversion of e-mail from IMAP to Exchange servers to the new
Apple-Exchange 2007 Web Services approach in another post.

I did have to specifically upgrade Microsoft's Remote Desktop connection
product as it had not auto-updated (or informed me) to its [recent
release][3].  It may be it just needed a "re-install" to insert special bits
somewhere.

Like [others][4], on one machine wanted to know where System Events.app was.
I was presented a GUI to browse to the file (and found it it in
System/Library/CoreServices.)

A few of the Mail.app plug-ins have not been upgraded yet.  These were
automatically disabled.

The DVD includes the latest Xcode (3.2) which I installed and Rosetta which is
an option item which I did not do yet.  I am going to try to do without the
old programs that only work natively on the PowerPC.  We will see.

Thank goodness Quicksilver still works.  That would be a loss even though
there is a new Google tool that is similar.  I modified it to search
/Developer for type com.apple.application to pick up those tools on one
machine -- evidently I had already done it on my other development machine.

I turned Time Machine off on the one machine I use it on during the update and
for a couple days in case of the need to retreat.  I have restarted Time
Machine, but as one would expect, it is taking a while to catch up to such
massive changes to the disk.  Another approach would have been to flush the
past and just start the drive over.

Like others, I use applications hosted in Oracle.  Those applications are not
yet certified for Java 1.6 and one of them did not work with Safari at a
critical point in the application.  I found that if I set Safari to run in
32bit mode (most of my machines are Intel Duo Core 2 and thus 64 bit capable
to one degree or another), that the application worked as it did before the
upgrade. To choose 32bit mode, select the application in Finder, and then "Get
Info".  On the pane, there is check box to run in 32 bit mode.

I have verified I can do SMB connections to printers and servers as well.

On one machine I had to fix my MacTeX installation in a minor way as
[described by the MacTeX folks at Tug][5].

I'll update this post if I remember (or encounter other things) in a bit.

All in all, much less traumatic than the move to Leopard and we will stay away
from discussion migrations in other OS's.

**Update 9/16/09:** There seems to be a new 32b version of Java 1.6 in Snow
Leopard and there is no other version.  So while I had the experience reported
above, it seems I don't have an understanding of "why" and at this point,
after 10.6.1 patch (if that matters), my Oracle application is working in both
32bit and 64bit modes of Safari.

   [1]: http://images.apple.com/macosx/images/buystrip_snow_box_20090824.jpg
   [2]: http://www.macosxhints.com/article.php?story=2009082703155512&query=ipsec%2Bpassword
   [3]: http://support.microsoft.com/kb/974283
   [4]: http://aloiroberto.wordpress.com/2009/08/29/snow-leopard-system-events-app-resolved/
   [5]: http://www.tug.org/mactex/faq/#qm10

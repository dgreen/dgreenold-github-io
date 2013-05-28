---
layout: post
title: Mail.app notes in Exchange 2003 (at least)
tags: 
---
When I started trying to use the new Notes feature in Mail.app, I was having
trouble with them _not_ being stored on the Exchange server.  I found that I
needed to make a Make a top level folder:  Apple Mail To Do"  and cause a
resync of the mail subsystem.  To cause the resync, I renamed ~/Library/Mail
to Mail-to-delete .

Note that later I had a bit of fun when deleting "Mail-to-delete" with
Spotlight but reseting that worked as well.

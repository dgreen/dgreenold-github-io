---
layout: post
title: Snow Leopard - Mail.app
tags: 
---
I have been using Apple's Mail.app as my client to talk to the University's
Exchange 2007 server.  I really don't like the monster database file that
Microsoft's Entourage product uses which is not friendly to incremental
backups.  I have been using the IMAP protocol for Mail, forgone task,
calendar, and contacts synchronization, and since I sync my iCal calendar with
Google's Calendar, I use Google's GSync on a dedicated PC to one-way sync my
calendar into Exchange.  This works because I am really only trying to show
other university calendar users my "Free-Busy" information not precise
details.

With Snow Leopard, Apple has included support for the new Exchange Web
Services interface that Microsoft has put into Exchange 2007 and that
Entourage (with the web services patch) has just started using.  Microsoft's
MacBiz Unit team has stated that the web services are Microsoft's long term
protocol for Exchange clients (Mac and PC) -- we will see about that.

Anyway, now Mail.app will use web services to interface with Exchange 2007 for
both incoming mail (and local synchronized store of same) and for outgoing
mail.  So there is no "SMTP" being emitted from the client machine.  This is
similar to the protocol footprint one has when using Google Mail either in a
web browser or using [MailPlane][1] as I usually do.

Additionally, one gets separate sections in Apple iCal and Apple AddressBook
to synchronize with the corresponding parts in Exchange.  One also picks up
groups scheduling with access to the free-busy information of other Exchange
users.  Right now, I am still thinking through if I will change my really well
working synchronization scheme to let Exchange fully participate.

[1]: http://mailplaneapp.com/


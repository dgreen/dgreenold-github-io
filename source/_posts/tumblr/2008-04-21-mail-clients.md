---
layout: post
title: Mail clients
tags: 
---
Boy, the trade-offs in Mac Mail clients can drive you crazy.  The Mail.app has
appealing features like templates, AOL presence detection, use of files to
store mail so backups can be incremental and access to ToDo's both on a IMAP
server and just in iCal.  Easier synchronization between multiple Macs.

However, Mail.app 3.0 can get confused.  When you are offline and take
actions, often you will get repeated mails on next connection.  Worse, and
perhaps Microsoft Exchange 2003 is also to blame, I have had cases where
messages on the Exchange Server just don't show up for a while even though
later messages do.  I don't know if it has happened often but I had a case
where missing some replies to a conversation was painful.  Mail and Exchange
also seem to have a bit of trouble with Drafts where mail saves drafts often
and Mail tags the older copies at deleted (but does not expunge them) and
therefore the number of messages in the draft folder is off.

Entourage in Office 2008 is a strong program, integrating with Microsoft
Exchange, appearing to handle off-line operation very well, and has good
editing ability of text messages.  It uses WEBDAV and is able to work on
connections that fade in and out.

The problems with Entourage include weak interoperability with the Apple
datastores for iCal and Addressbook. One could do without it at Entourage 2004
but there is no longer a separate connector for Entourage.   Entourage insists
on exporting text files with the old (pre-OS X) line ending convention (sigh).
Entourage uses a large database for the primary mail store so incremental
backups like SuperDuper! and TimeMachine don't work well.  TimeMachine must be
set up to ignore it or the many duplicates that it creates will eat the
available disk space.   Entourage also stores the connections relating
messages and other items locally so they are lost if you work with another
machine regardless of what software you use.  They can also be lost on various
"events" that have occurred between Exchange and Entourage in the past.

Tonight, I am using Entourage 2008 on my main machine which I carry around
everywhere and use Exchange OWA for the odd cases for mail that are on other
machines.  I also am looking at moving more and more "personal" mail to GMAIL.


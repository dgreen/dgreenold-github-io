---
layout: post
title: Normal OS X users can't, by default, use sudo
tags: 
---
As the MacDefender phishing installing malware becomes prevalent, folks are
repeating security advice such as the following from MacFixit (of the CNet
organization):

> If your working account is an administrator account, you can convert it to a
non-admin account very easily, and this will not change the way your system
runs at all. All it will do is require administrative credentials to perform
certain tasks that otherwise could have been done without supplying
credentials. As a result, your system will notify you if a program is trying
to modify some system resources that would otherwise be freely editable if you
were running in an admin account. To convert your account to a standard one,
go to the Accounts system preferences and create a new account that will be
your new administrator account. Give it a name and a password, and ensure that
it has administrator capabilities. When the new administrator account has been
made, log out of your current account and into the new admin account, and go
back to the Accounts system preferences. Click the lock and authenticate your
new admin credentials. Now select your old account and uncheck the box for
"Allow user to administer this computer." Now log out of your new admin
account and back into your old account, and you're good to go: you should be
safer from these types of malware threats.

Geeks should note that "normal users" can't use sudo at the command line
without hacking the Mac environment a bit. I have not seen this limitation
mentioned. For some, this adds a "con" to removing admin authority to normal
user account.


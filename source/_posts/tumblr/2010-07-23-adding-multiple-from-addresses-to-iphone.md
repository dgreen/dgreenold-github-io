---
layout: post
title: Adding multiple from addresses to iPhone
tags:
- ios
---
For me, it it is adding an @IEEE.org as an alternate from: address in the
iPhone mail client associated with a Google gmail account.

One approach is given here: [http://modernerd.com/post/535350679/solved-gmail-
ipad-iphone-and-multiple-from][1] . It worked with iOS 3.0 but does not seem
to work any longer.

An alternate approach is to create a fake pop3 account which sends through
Google and uses a fake pop3 server account. I used the server mail.xyz for the
server name. To avoid as many messages about the fake pop3 server not
responding as possible, set it's check mode to manual. Alas, in iOS 4, there
will still be some.

[1]: http://modernerd.com/post/535350679/solved-gmail-ipad-iphone-and-multiple-from


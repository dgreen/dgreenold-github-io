---
layout: post
title: ! 'Feed the google: ie7 png jpg MIME confusion'
tags: 
---
So DavidB and I are working on a new bug in OUMgt -> folks can't upload .jpg
and .png files into our RAILS app. This used to work.

After a bit of exploring (much more for the PNG issue than the jpg issue, and
actually the help of gracious Internet developer), we have found:

IE7 marks x.jpg with the Mime type of image/pjpeg and marks the file x.png
with the Mime type of image/x-png .

Sigh.


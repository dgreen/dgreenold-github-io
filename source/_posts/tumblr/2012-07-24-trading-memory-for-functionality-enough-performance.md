---
layout: post
title: Trading Memory for Functionality (Enough Performance)
tags: 
---
I was working on a the last note and wanted to check things out under a fresh
install. I decided to make a new Mac User to accomplish this. I used GitHub
for the Mac, Safari on the Assembla site and the Tumblr site, and the command
line. When I finsihed my work, I idlely was thinking about keeping this user
account around for the next effort or deleting it. One of the consideration
was how much space was in use by the account. I was shocked to see that the
home directory took 330MB!

Looking into it, I found the bit space was 300MB in Preferences. The other two
large directories was Caches (30MB) and Applications Support (12MB). Inside
preferences was a folder SMDHelpData that was the space user. This folder
evidently has the help file information: info, caches, and indexes for finding
things for all the applications on the system (not just those that had been
used). I am guessing there is a distinct copy per user since in theory at
least, one could through security settings block different users from various
components. There may also be some personalization (highlighting, last
location, etc.) capability.

I was very surprised at how much space was taken but I decided my lesson was
to also trade space for functionality (enough performance) and leave the user
configured so I would not spend time repeating the building of this space.


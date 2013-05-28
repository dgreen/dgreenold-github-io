---
layout: post
title: Git and DropBox Together
tags:
- Dropbox
- git
---
There are several posts about using DropBox for the remote repository for Git.
I wanted my local Git repository on DropBox to share between machines with a
remote repository supported in Assembla (or GitHub). It is really not a
problem to do:

  1. Create the space in DropBox using one machine and take the right steps to
connect it to the remote repository. There are lots of scenarios here but they
are covered elsewhere and not the focus of this note.

  2. Wait for DropBox and the two (or more computers) to catch up.

  3. Everything should be good EXCEPT DropBox does not propagate Unix File
Permissions and Git tracks these as well as file contents.

  4. On the machine(s) that were not the machine used in step 1 (and before
making any changes to the initial checkout, do a

`git reset --hard HEAD`

to get Git to reset the file permissions.


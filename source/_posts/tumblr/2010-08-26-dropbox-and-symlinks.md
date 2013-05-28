---
layout: post
title: Dropbox and symlinks
tags:
- Dropbox
---
Symlinks don't work well with Dropbox. They cause unexpected unrolling of the
symlink on the clients that don't originate the symlink.

Symlinks (or what I am calling symlinks -- symbolic links) are made on Unix
like systems using

    ln -s original-path  symlink_name

or GUI tools that do the equivalent.

This works on the machine where the command is done but on the remote
machines, they copy the original file referred to by the symlink. Of course,
if the symlink is a directory it is a very large replication of content which
one was probably trying to avoid by the original symlink.

In defense of Dropbox's approach, Windows machines don't honor symlinks so
without replication of the original content, there would be no access. And, of
course, others think this is a [feature][1].

[1]: http://wiki.dropbox.com/TipsAndTricks/SyncOtherFolders


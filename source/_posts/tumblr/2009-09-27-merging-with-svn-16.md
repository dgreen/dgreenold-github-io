---
layout: post
title: Merging with svn 1.6
tags:
- subversion
---
Lots of work has been done by the Subversion team (probably in response to
Git).  One can now do a merge from a project branch back into the main trunk
rather easy:

`svn merge ^/tags/version-1.6.1/`

will merge changes in 1.6.1 not in the trunk.  The ^ is relative remote
addressing.

**Update:**

Another example:

`svn merge --dry-run --revision 944:945 ^/trunk/oumgt/`

will show you the actions that would be taken if one asked to merge revision
945 from the trunk/oumgt/ space into the present present space.

**Update 2:**

Related example:

`svn merge --dry-run ^/trunk/oumgt/`

will show you the actions that would be taken if one wishes to apply all
revisions in trunk/oumgt/ space but not in the present present space.

**Update 3:**

SVN is still limited in how it can track changes and moving things back and
forth will eventually cause trouble. In short, one should decide to mostly
merge in one direction. The approved way to merge in the opposite direction is
to do a "--reintegrate" merge after which one should no longer use the branch
merged from. This page describes things at [SVN 1.5][1]

[1]: http://blogs.open.collab.net/svn/2008/07/subversion-merg.html


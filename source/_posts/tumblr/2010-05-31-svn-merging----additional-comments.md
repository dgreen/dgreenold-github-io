---
layout: post
title: svn merging -- additional comments
tags:
- svn
---
This is a small expansion on an earlier [post][1] about svn merging.

The svn [Red Book][2] gives the typical scenarios for merging including
supporting work in development branches.

Create the branch:

    svn cp https://svnserver.com/app/trunk https://svnserver.com/app/development

Check it out

    svn co https://svnserver.com/app/development

Do work and keep the local copy updated based on updates to branch, trunk

    blah
    svn up
    svn merge [--dry-run] ^/trunk

Commit changes (including those merged from trunk

    svn ci

When done, merge back to trunk, delete branch, remake branch

    svn merge [--dry-run] --reintegrate ^/branches/development
    svn ci
    svn delete ^/branches/development
    svn cp https://svnserver.com/app/trunk https://svnserver.com/app/branches/new-development

In chapter 4 of the RedBook is a section called "Reintegrating" where the
authors discuss why one should delete the development branch (and if necessary
recreate it).

[1]: /2009/09/27/merging-with-svn-16.html
[2]: http://svnbook.red-bean.com/nightly/en/svn-book.pdf


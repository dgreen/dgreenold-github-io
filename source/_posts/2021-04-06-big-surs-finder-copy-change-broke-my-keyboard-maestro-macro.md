---
layout: post
title: "Big Sur's Finder Copy change broke my Keyboard Maestro macro"
date: 2021-04-06 22:47
comments: true
categories: macos, productivity
---

In Catalina, Copy in Finder gets the path of a file.  In Big Sur, it only gets the filename.  One can hold down ⌥+⌘+C (or ⌥ and select Copy from the Finder menu) to copy the pathname but Keyboard Maestro does not "Copy as pathname" as an action or option of its Copy action.

I had built  ⌃+⌥+⌘+U to put a URL style address of a file or folder currently select in  Finder to the clipboard.   I used to paste in file references that I could later reference as noted in a [prior note](/blog/2020/12/29/open-by-highlighted-url/) but the upgrade to Big Sur broke this.

<!-- more -->

I had used

{% img /images/20210406-old-kbm.png "My Broken Keyboard Maestro Macro" %}

but as I note above Finder's interpretation of Copy has changed.

I could not find a Copy Pathname option in Keyboard Maestro (or anyone mentioning the change in Finder).  I tried asserting the modifier ⌥ with press and hold but it did not seem to modify the copy behavior.  I tried sending the key ⌥+⌘+C to finder but it seem to bring up Keyboard Maestro like ⌥+space does.

{% img /images/20210406-new-kbm.png "My Updated Keyboard Maestro Macro" %}

This works but it does have a side affect of processing each of the selected items (with the clipboard left with the final result.  To be honest, that may have been the behavior of the old process under Catalina as a multiple selection was not tried.
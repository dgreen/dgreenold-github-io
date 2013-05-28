---
layout: post
title: "Exploring stately for Ruby"
date: 2013-01-19 01:24
comments: true
categories: 
---
As someone who has built a hardware-based Morse Code sending system, I am very interested in state machines and their implementation.

I recently found a new ruby gem [stately][1] which seemed interesting.  Like many packages, the documentation initially seemed confusing so a bit of exploring seemed appropriate.  This note documents the little exploring that I did (mostly so I can return to it should I want to use this gem in an application.  The two examples left when the dust settled are given in this [gist][2].

My first attempt was to build a counter.  I had a bit of problem getting the syntax right and when I retreated to the document's examples,  I found they were incomplete.  My first successful attempt (from a syntax point of view was stately_demo_bad (see the [gist][3]).

It did not work because the method associated with defining all the details of the state machine appears to change the scope of some of the code into other internally defined classes yielding very unexpected behavior.

Moving everything to method (messages) inside the state machine seems to be the expected (and allowable) approach yielding stately_demo_good (see the [gist][4]).

[1]: https://github.com/rtwomey/stately
[2]: https://gist.github.com/dgreen/d08cbdf7e52ed2cf0074
[3]: https://gist.github.com/dgreen/d08cbdf7e52ed2cf0074#file-stately_demo_bad-rb
[4]: https://gist.github.com/dgreen/d08cbdf7e52ed2cf0074#file-stately_demo_good-rb

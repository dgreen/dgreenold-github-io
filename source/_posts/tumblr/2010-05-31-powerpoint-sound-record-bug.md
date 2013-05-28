---
layout: post
title: Powerpoint Sound Record Bug
tags: 
---
Sometimes you think you are going crazy only to find out it is a software bug
(or feature!).

I was trying to update the audio for a _Powerpoint_ slide presentation. I set
the record volume to the level I liked in OS X with the Sound Preference
Panel. I also set up the nice USB microphone to be the source of the sound.

Then I selected `Insert | Sound | Record` to bring up the _Microsoft
Powerpoint 2008_ widget to record the sound. I was not getting good sound
levels. Eventually I left the _Apple_ Sound Preference Panel displaying the
sound level and discovered that when I hit the `Record` button, the sound
level was lowered automatically. Once I figured it out, I was able to counter
the behavior by revisiting the Sound Preference Panel after hitting record. Of
course, it is hard to hit record, give the Sound Preference Panel focus, and
read a slide's script with out delay and at a level volume but it was good
enough (or I was giving in).

I tried building an _Automator_ workflow to do this and I could get it to
record hitting the `Record` button but evidently _Microsoft_ did not give them
unique names so the recorded action would not active the record button. Had I
been able to do that, there was an _Apple_ insert for _Automator_ to allow me
to reset the audio level.


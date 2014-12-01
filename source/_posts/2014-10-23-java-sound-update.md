---
layout: post
title: "Java Sound Update"
date: 2014-10-23 22:24
comments: true
categories: 
---

For years, I have been using (and advising the use of sun.audio) for playing sounds in the Java VM
using [Alvin Alexander's article][oldstyle] for inspiration.  The downside of this approach, of course,
is the dependency on classes that are not part of the JAVA API and therefore might change at anytime
although they have been relatively stable for many years.

Recently, I found a [stackoverflow discussion][newstyle] noting the existence of AudioSystem (and related clases).

```java
/*
 * File: ModernRingPhone.java
 * Author: David Green <dgreen@uab.edu>
 * Assignment:  SoundOff - EE333 Fall 2014
 * Vers: 1.0.0 10/23/2014 dgg - initial coding
 *
 * Credits:  Concepts from http://stackoverflow.com/questions/15475276/short-sound-file-plays-in-netbeans-but-not-in-jar
 */

import java.io.File;
import java.io.FileInputStream;
import java.io.InputStream;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.Clip;

/**
 *
 * @author David Green <dgreen@uab.edu>
 */
public class ModernRingPhone {

  public static void main(String[] args) 
  {
    try {
        // open the sound file as a Java input stream
        String gongFile = "telephone-ring-3.wav";
        InputStream in = new FileInputStream(gongFile);

        // create an audiostream from the inputstream
        Clip clip = AudioSystem.getClip();
        clip.open(AudioSystem.getAudioInputStream(new File(gongFile)));

        // play the audio clip with the audioplayer class
        clip.start();
        
        // wait for sound to finish before terminating program (necessary for 
        // running inside NetBeans, at least)
        Thread.sleep(10000);
    }
    catch ( Exception e) {
        System.out.println("Things did not go well" );
        e.printStackTrace();
        System.exit(-1);
    }
  }
}

```


[oldstyle]: http://alvinalexander.com/java/java-audio-example-java-au-play-sound
[newstyle]: http://stackoverflow.com/questions/15475276/short-sound-file-plays-in-netbeans-but-not-in-jar



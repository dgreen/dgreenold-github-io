---
layout: post
title: "Java Sound Update 2"
date: 2015-12-10 20:22
comments: true
categories: 
---
This is an update to a prior [article](https://dgreenteach.org/blog/2014/10/23/java-sound-update/).

UAB EE Students Andrew Peturis, Chaselyn Langley and other team members produced an interesting 
GUI Application for children to associate sounds with images.  In the course of doing this, they
wished to expand the control of the audio beyond my original example.  They discovered a bit of
behavior that was not (at least clearly) documented in the JAVA API.

They modified the original demo substantially for their application and supplied a limited
version of it to me as an update to benefit future classes (as well as the broader Internete
Community).  I merged their two classes into one focused only on the sound system behaviour and
hopefully preserved the important behaviors they wished to document.  The new code is show below.

```java
/*
 * File: Sound.java
 * Authors: Andrew Peturis, Chaselyn Langley, David Green
 * Vers: 1.1.0 12/10/2015 dgg - update example to standalone
 * Vers: 1.0.0 10/20/2015 agp - initial coding
 *
 * Credits:  Team SoundBox - EE333 Fall 2015
 */

import java.io.File;
import java.io.IOException;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.Clip;
import javax.sound.sampled.LineUnavailableException;
import javax.sound.sampled.UnsupportedAudioFileException;

public class Sound {

    private String sound;
    private Clip clip;
    private boolean isPlaying;  // Sound loaded up and has started playing (may be paused)
    

    // Don't allow default constructor
    private Sound() {
    }

    public Sound(String sound) {
        this.sound = sound;
        isPlaying = false;
    }

    // Play a sound using javax.sound and Clip interface
    public void play() {
        try {
            if (!isPlaying) {
                // Create a clip to hold a sound
                clip = AudioSystem.getClip();
                clip.open(AudioSystem.getAudioInputStream(new File(sound)));
                isPlaying = true;
            }
            // Play the audio clip with the audioplayer class
            clip.start();
        } catch (LineUnavailableException | UnsupportedAudioFileException | IOException e ) {
            System.out.println("Things did not go well");
            System.exit(-1);
        }
    }

    // Continue a stopped sound
    public void resume() {
        if (isPlaying) {
            clip.start();
        }
    }

    // Pause a playing sound
    public void pause() {
        // clip.stop() will only pause the sound and still leave the sound in the line
        // waiting to be continued. It does not actually clear the line so a new action could be performed.
        if (isPlaying) {
            clip.stop();
        }
    }
    
    // Stop a sound from playing and clear out the line to play another sound if need be.
    public void end() {
        if (isPlaying) {
            pause();        
            // clip.close(); will clear out the line and allow a new sound to play. clip.flush() was not 
            // used because it can only flush out a line of data already performed.
            clip.close();
            isPlaying = false;
        }
    }

    // Small demo program
    public static void main(String[] args) {
        Sound sound = new Sound("predator.wav");
        try {
            sound.play();
            System.out.println("Playing for 1 second");
            Thread.sleep(1000);     // let it play a second
            sound.pause();          // pause
            System.out.println("Pausing for 5 seconds");
            Thread.sleep(5000);     // continue playing
            System.out.println("Playing for 1 second");
            sound.resume();
            Thread.sleep(1000);      // play have a second
            System.out.println("Ending, resuming which should silently fail");
            sound.end();            // End sound
            sound.resume();         // Should be silent
            Thread.sleep(5000);     // Wait 5 seconds
            System.out.println("Playing again for 5 seconds");
            sound.play();           // Should start again
            Thread.sleep(5000);
            sound.end();
        } catch( InterruptedException e) {
            // just fall to end
            // System.exit(0);
        }
    }
}

```

### Update February 2020

Changed my web site server link.
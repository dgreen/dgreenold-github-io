---
layout: post
title: Adjusting the Mac OS X path
tags:
- java
- os x
- command line
---
The **path** is an environmental variable that tells the command line (shell)
processor where to look for programs (commands) to run when they are entered
on the command line without any directory information. The shell will look for
the command in all the directories listed in the path variable.

In OS X, the active path can be shown when in the terminal window by typing
`echo $PATH` command on the command line (where `[user@system ~]$` is the
command line prompt and the text right before the "]" is the present working
directory (pwd). If it is "~" then it is the home directory of the user,
typically something like /Users/user (for a user named user).


     [user@system ~]$ echo $PATH


The path in OS X is maintained in several places:

  * .bash_profile
  * .bashrc
  * system versions of the above
  * .MacOSX/environment.plist

There a lot of references for the first three since this is roughly the same
as Linux/Unix assuming both systems are using the bash terminal shell. An
example is in [Tech-Recipes][1].

.MacOSX/environment.plist is obviously specialized to OS X, and this path
modification is seen by the GUI as well as command line programs run in the
terminal window. If the directory does not exist, you can make it at the
terminal prompt:

    [user@system ~]$ mkdir .MacOSX

Today, the file, if it exists, may be stored in binary rather than in text
form:

    [user@system ~]$ cd .MacOSX
    [user@system .MacOSX]$ more environment.plist
    "environment.plist" may be a binary file.  See it anyway?


is indicative of the file being binary. The command `plutil` can convert this
binary file to text oriented:

    [user@system .MacOSX]$ plutil -convert xml1 environment.plist

at this point, you can edit it carefully to contain your path. It must be a
complete collection where each path is separated by a ":" and the file must
obey XML rules. Mine looks like:


    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>PATH</key>
        <string>/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/X11/bin:/opt/local/bin</string>
    </dict>
    </plist>

You can either edit the file by hand with your favorite text editor, or if you
have Xcode installed, there is a tool to edit the file in a structured manner.
The tool may be able to work without conversion from binary to xml.

After editing the file, you may wish to convert it back to binary (although I
don't think it is necessary) by

    [user@system .MacOSX]$ plutil -convert binary1 environment.plist

After changing this file, you will have to either logout or reboot so that all
the OS X parts associated with your login will use this new path.

* * *

### Short note for other OSes

The JAVA folks offer this [short article][2] for other operating systems such
as various versions of Windows, Linux, and Unix.

[1]: http://www.tech-recipes.com/rx/2621/os_x_change_path_environment_variable/
[2]: http://java.com/en/download/help/path.xml


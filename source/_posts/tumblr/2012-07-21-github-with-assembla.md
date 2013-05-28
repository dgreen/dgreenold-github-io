---
layout: post
title: GitHub with Assembla
tags: 
---

[GitHub][] has now made a nice simple GUI tool for both [OS X][1] and
[Windows][2]. They have made them freely available for download. They seem to
have made careful choices about what to support and not support in order to
keep tool as simple as possible. They do support using GitHub[^fn1] against
other git repositories such as Assembla or a homegrown one. They don't support
multiple remote repositories for a specific local repository but you are free
to use GitHub.com for one project[^fn2] and Assembla (for example) for
another. The two limitations that I have seen that "hurt" sometimes are

  1. There is no graphical view of the change tree (while confusing, if you need it, alternatives are even more confusing)
  1. The Windows and Mac Clients look different and behave a bit different.
  1. Github really knows you by the name/email you list in it's configuration and does not like/support your having a separate identity on a per project basis.

These limitations are not fundamental and Github.com may work on them in the
future. There have been frequent updates thus far to Github -- perhaps they
will continue.

## Using GitHub with an existing project hosted in Assembla

If this is your first use of Assembla (but assuming you already have an
account), then you will need to update your Assembla profile with your public
ssh key. This file may exist on your system `~/.ssh/pub.rsa` where `~` refers
to your home directory. You probably generated this as part of your git
install but if not (and after you possibily install ssh), use


    ssh-keygen -C "demo@example.com" -t rsa

substituing your email address. Take the defaults (hit return) on everything
unless there is an offer to overwrite the pub.rsa file AND you need the pre-
existing one! You will now a the file you need. Go to your profile in
Assembla, select manage keys and upload this file to assembla.

If there is no local repository associated with the existing project, you will
need to clone it using the command line. Assembla gives the step by step
instructions personalized for the repository (see the "git clone" information
near the top of the Source/Git tab). Be sure to use the "clone/push URL" if
you are planning to push back to Assembla in the future.

After you have a local repository (start here if you already had one), merely
start up GitHub, and use the menu to select `File | Add Local Repository`
option selecting the directory containing the project repository.

## Starting a new project with GitHub and Assembla

Make your Assembla Space in Assembla selecting an option that includes
Source/Git repository. After it is made, you will be on a page that contains
very useful "Getting started with Git" instructions. For this note, I assume
you have installed git and configured it with your name and email.

If you are starting the project, create your repository folder as you would
any folder, perhaps


     mkdir demo


Attach a terminal window to this new directory (new project) or the existing
directory corresponding to the top of your existing project.


     cd demo


Then, assuming you have not been using git and a local respository only,
initialize git


     git init


If you have a new project, you need at least one file. Create one -- prehaps a
readme.txt file.


     echo "" > readme.txt


Out of scope for this note but if it is an existing project not yet in git,
you may wish to [set up a .gitignore file][5] to keep certain files (or file
types) from being tracked. We will assume we are tracking everything for
simplicity here.

Now, we need to add all new (or changed files)_for tracking and commit the
present state of the files to the local repository. We will use "First commit"
as the message about this commit. Adjust as desired but limit yourself to one
line of information unless you know how to do multiple lines as one command in
your terminal (command) program.


    git add .  
    git commit -m "First commit"


Now configure the repository to know where the remote repository is in
Assembla. Be sure to use the customized one on your Assembla instructions.


    git remote add origin git@git.assembla.com:demo.git


where demo is the name of the remote repository as known to Assembla.

Finally, send your first commit up to the remote repository.


    git push origin master


Success. You can now switch to Github as noted for an existing git reponsitory
above.

* * *

  [^fn1]: I will use "GitHub" to refer to the program and "GitHub.com" to refer to the site or company for the remainder of this note.

  [^fn2]: Don't forget to create your Github.com account and tell GitHub about this!

[Github]: http://github.com
[1]: http://mac.github.com
[2]: http://windows.github.com
[5]: https://help.github.com/articles/ignoring-files


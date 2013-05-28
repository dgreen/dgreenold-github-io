---
layout: post
title:  "Tumbling out!"
date:   2013-05-27 23:02:45
categories: blog update
---

In a long overdue action, I have moved the glimmer blog out of Tumblr.  I had
been wanting to use [(Multi-)Markdown][mmd] more in blogging to continue my
focusing on the format.  I also had a student tell me he could not access the
Tumblr website at work due to its other content.  Tumblr was/is an easy to use
site but my purposes and those of other users don't seem to match.  I had been
looking at Jekyll for a while and considering what to try when I discovered
that GitHub supported web hosting with some support for Jekyll.  Finding the
[Jekyll importer][importTumblr] that would do most of the heavy lifting for
moving the site, I took the plunge.

Over about 4 hours, I was able to do fixups of the files that the importer
brought over.  I also changed Jekyll to use Kramdown instead of Maruku based
on  this [hint][] originally from [Brett Terpstra][brettterpstra].

After a bit more exploring, I discovered Octopress which wraps Jekyll with
additional conveniences (even though it uses an older version of Jekyll).  I
was able to copy the raw Jekyll work into the [Octopress][] copy.

After trying things out, I also made the decision to host against my Github
Account rather than a project (although both Jekyll and Octopress can handle
either approach.)  This was a bit hard to retreat to.  I had to

  1. Re-run scripts
  1. Edit .git/config
  1. Edit Rakefile
  1. Edit _config

but I think I got it.

Most "irritating thing" is to put `bundle exec` in front of all rake commands
as Octopress is not using more current code.  I have not generally had to 
worry about that in the past but I know many others have.

[importTumblr]: http://jekyllrb.com/docs/migrations/
[hint]: http://natedickson.com/blog/2013/04/09/mostly-multimarkdown-blogging-in-octopress/
[brettterpstra]: http://brettterpstra.com
[mmd]: http://fletcherpenney.net/multimarkdown/
[Octopress]: http://octopress.org/ "Octopress"





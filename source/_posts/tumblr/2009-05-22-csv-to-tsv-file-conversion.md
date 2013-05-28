---
layout: post
title: CSV to TSV File Conversion
tags: 
---
I having been keeping three office suites (MS Office 2008, OpenOffice.Org, and
iWork) on the MacBook Air I use.  After looking at the interoperability
glitches between MS Office (which IEEE uses broadly) and OpenOffice.Org, I
decided to consider removing OpenOffice.Org to reclaim disk space which is at
a premium on the Air.  The big reason I keep OpenOffice.Org around is to
create Tab Separated Files that I use in several workflows.

In several workflows, including the Region 3 Meeting Registration Application
and my course plan to syllabus product for the university, I use a spreadsheet
for development of information and then export the information to a tab-
separated value file for processing by scripts as needed.  I use tab-separated
files because tabs don't occur in my data and thus it is a good separator.
OpenOffice's Calc (their spreadsheet) can write a decent tab separated file.

Alas, Microsoft Excel on the Mac did not use to have a tab separated output
(only comma separated output).  Now, Excel 2008 on the Mac now has a tab
separated output but it has two issues:

  1. The tab separation appears to have merely substituted tabs for commas in
the output file.

  2. Microsoft still has not gotten the word that OS X uses the linefeed code
( ) like UNIX not a carriage return code ( ) like OS 9 and incorrectly marks
its output lines.

The flawed tab separation output adds quotes around cells that contain commas
and doubles quotes within quotes  for data transparency.  This is added
complexity to parse and is the reason I was avoiding the CSV format.  I did
not want (in my existing code) to deal with CSV or the MS flawed TSV format.

Looking around the web, I did not find a utility to do the conversion but I
noticed support for the [CSV support in Ruby][1].  A general translation of
CSV to TSV (where operating system newlines are supported by the language
implicitly can be done neatly with

    #!/usr/bin/env ruby

    require csv

    if ! ARGV[0]
      puts "Usage: csv2tsv file.csv  (writes to standard out)"
      exit
    end

    CSV.open( ARGV[0], r) do | row |
      puts row.join("   ")
    end

and a slight change to the open method can fix change the input reading to use
carriage return line endings while outputting using OS line endings.  The
resultant code with modification is

    #!/usr/bin/env ruby

    require csv

    if ! ARGV[0]
      puts "Usage: csv2tsv file.csv  (writes to standard out)"
      exit
    end

    CSV.open( ARGV[0], r, nil, " ") do | row |
      puts row.join("   ")
    end

Since I had to unescape the cells anyway, I chose to start from the more CSV
rather than the uncommon version of TSV  output by Excel 2008.

A future improvement could be to auto-detect the line ending problem.

[1]: http://www.ruby-doc.org/core/classes/CSV.html (CSV support in Ruby)


---
layout: post
title: MultiMarkdown
tags: 
---
I have been using [_MultiMarkdown_][1] for a while now. I use it for creating
simple text files that I want to read in text mode but also want to perhaps
"dress up" as either a HTML or PDF file (mostly the former).

Since it is text oriented, it is easy to use scripts to automate things into
or within this format. Many of my UAB pages are built with it (I use a .mmd
file extension) and I built an extensive set of scripts and processes for
maintaining _IEEE Region 3_ meeting agendas with the tool. I successfully
turned this package over to the new _Region 3 Secretary_ so there is now "user
2" for this automation.

The _MultiMarkdown_ site has a good documentation as well as some files to
download as examples. For my course [web pages][2], I use a banner to provide
breadcrumb like linkages to other parts of the university, my department, and
my web site. This banner as well as the heading of one of my typical
_MultiMarkdown_ pages looks like

* * *


    Title:        What Tools Do I Need?
    Author:       David Green
    Affiliation:  UAB
    Date:         DATELM
    Keywords:
    Format:       complete
    LaTeX XSLT:   article.xslt

    [UAB][1] -> [ENG][2] -> [ [ECE][3] / [ECE Intranet][4] ] -> [ [DGreen][5]
/
    [DGreen Intranet][6] ] -> [EE448/548][7] -> TITLE

    * * *

    TITLE
    =====

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc vestibulum
facilisis
    justo, eget tempor ligula accumsan nec. Proin dignissim fermentum
scelerisque.
    Donec scelerisque vehicula dui ac imperdiet. Integer est dolor, varius
dapibus
    ultricies a, facilisis sed tortor.

    Fusce quis orci turpis, eget fringilla arcu.
    Quisque a ligula a tellus commodo gravida dapibus nec massa. Fusce eu urna
lacus,
    ac molestie odio.

* * *

I use a script to process `TITLE` to match the title in the header as well as
change the text `DATELM` to the present date. My script, after doing some
substitutions like the ones described, calls the _MultiMarkdown_ script
`mmd2XHTML` which generates the web page.

By removing, the header through the `TITLE` (and its underline) lines, it can
be processed using the _MultiMarkdown_ script `mmd2PDFXeLaTeX.pl` to produce a
nice looking _PDF_ document.

Finally, I should note that many blogs (including _tumblr._) accept
[_Markdown_][3] formatting which is the initial motivation for the
_MultiMarkdown_ tools.

[1]: http://fletcherpenney.net/multimarkdown/

[2]: https:/dgreenteach.org/DGreen/ee448

[3]: http://daringfireball.net/projects/markdown/

### Update February 2020

Changed my web site server link.
---
layout: post
title: "Making BookMarked PDFs from Google Docs"
date: 2020-05-25 11:28
comments: true
categories: 
---

This post focuses on ensuring that the Table of Contents, as set up using Google Docs index, are transferred into the bookmark metadata of the PDF file.  This can not be done by simplifying downloading a Google Doc as a PDF. One must export to a `.docx` file and use Word, Writer, or Pages to produce the PDF file using the correct options for each program.

Using macOS Preview as the PDF reader, we want the left sidebar when one selects Table of Contents to show the Table of Contents as bookmarks that allow quick access to the page where the content is.

{% img /images/sidebar-toc.png 'Preview showing sidebar with Table of Contents selected and results' 'Choose Table of Contents in sidebar' %}

<!--more-->

## Background

I have chosen Google Docs to maintain the IEEE Region 3 Operations Manual. IEEE is a GSuite organization, and I feel that using GoogleDocs had the best potential for promoting collaboration on documents. Additionally, it provides a cloud-based approach for ensuring the source content is available over time. One issue that arises from this choice is the reduced feature set in Google Docs as compared to Microsoft Word, LibreOffice Writer, and Apple Pages.  Google Docs is growing to support more features over time, and the others (especially Microsoft and Apple) are trying to ensure consistent feature sets across all platforms (desktop, smartphone, web) -- the gap is closing.

## Process that works

TLDR;

> Google Doc → download as .docx → use word processor with bookmark/accessibility options → PDF

The process that works is to download the file from Google Docs as a `.docx` file.  Then using Word, Writer, or Pages open the file and then export it to PDF choosing to use the accessibility options. My computer is a MacBook Pro 13 2018 and is presently running

* MacOS Catalina 10.15.4
* Microsoft Word 16.37 (from a Microsoft 365 subscription)
* LibreOffice 6.4.4.2
* Pages 10.0 (6748)

The result we are seeking is to have the table of contents information inserted and maintained in Google Docs.  It should not only appear in the PDF page but also appear in the metadata of the PDF file so that users can quickly jump to those sections.

After using the heading styles in your document to denote the structure, insert the table of contents in the appropriate part of your document using the menu option *Insert → Table of Contents*. Choose to show numbers rather than links if you wish to support printed versions of the PDF. Make sure you are adding page numbers to your page (use the menu option *Insert → Page Numbers*). The table of contents should now be visible in the document. Right-clicking on the table of contents allows you the option to refresh the table of contents after document changes. You should also be able to click on an entry and select the link to jump to that portion of the document for editing.

Using the menu option *File → Download → Microsoft Word (.docx)*, get a local machine copy of the document in `.docx` form. The next step is to open it in your tool of choice and create the PDF.

### Using Word

Open the downloaded `.docx` file in Word. Choose *File → Save As...* and then select PDF as the File Format and choose to use the online service.

{% img /images/word-pdf.png 'Using Word's File → SaveAs...' %}

### Using LibreOffice

Open the downloaded `.docx` file in LibreOffice (Writer). Choose *File → Export As → Export As PDF...* and then choose to export the bookmarks. The graphic shows the other options that I selected but not all of them may be necessary.

{% img /images/libreoffice-pdf.png 'Using LibreOffice Writer's File → Export As → Export as PDF...' %}

### Using Pages

Open the downloaded `.docx` file in Pages. Choose *File → Export To → PDF...* and choose to export using the accessibility option.

{% img /images/pages-pdf.png 'Using Pages's File → Export To → PDF..' %}

## Issues with Google Docs export

The most desirable workflow is for Google Docs to add the bookmarks from the Table of Contents to the PDF file or create the document in one of the tools (Word, Writer, or Pages) that will generate the desired PDF. Alas, this is not possible today.  Looking at the Google Support forums, it is clear this is a desired feature, so hopefully, it will appear one day.

In working towards a process to produce a PDF with bookmarks for the Table of Contents, I ran into two limitations in Google Docs. The working around the first limitation

> *File → Download → PDF Document (pdf)*: does not include the table of contents as bookmark metadata

has been the focus of this post.

I discovered an additional problem:

> *File → Down → Open Document Format (odf)*: does not export a proper Table of Contents index structure

This limitation (at least part of this is a bug IMO) means that the Table of Contents, made correctly in Google Docs, is not translated into Open Document Format correctly.  If you try to update the index, it shows nothing. It is not surprising then that it is not available for LibreOffice Writer to export the Table of Contents information as bookmark data. As noted above, LibreOffice Writer does work when using the`.docx` output file from Google Docs.

---
layout: post
title: ASP Code For YYMMDD timestamp
tags: 
---
OK, so maybe no one will ever need it but I did (or so I thought) so after not
finding code available, I wrote it.

Basically, I needed to make a timestamp in an old version of ASP.  There are a
few date string conversions in the VB of ASP but not the one I needed.  The
newer ASP.NET has a richer collection but that was not the engine of the day.

I ended up with a function:

    ' Convert number to string with leading zero if needed
    ' Accepts 0 and up
    ' if 0-9 return 00, 01, ... 09
    ' if > 10 < 99 return number as text
    ' if > 100, modulus number to between 0 and 99

    Function Return2CharForNumber( Value )
      TwoDigit = Value Mod 100
      If (TwoDigit > 9) Then
        Return2CharForNumber = CStr(TwoDigit)
      Else
        Return2CharForNumber = "0" & CStr(TwoDigit)
      End If
    End Function


which was used like this for a timestamp:

      ThisYear = Return2CharForNumber(year(date()))
      ThisMonth = Return2CharForNumber(month(date()))
      ThisDay = Return2CharForNumber(day(date()))
      TimeStamp = ThisYear & ThisMonth & ThisDay


Nothing to brag about but I wanted to put out there in case it was any use to
anyone (including me at a later time).

Now the sad truth, after writing it, debugging it, and deploying it -- the
interface changed back close to what was already in the code so the above is
no longer needed.

Sigh.


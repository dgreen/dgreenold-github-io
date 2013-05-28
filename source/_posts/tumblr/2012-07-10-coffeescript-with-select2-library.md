---
layout: post
title: CoffeeScript with Select2 library
tags: 
---
I had two demons: a new library and a language I was not really familiar with.
A formula for puzzles. I did not find quickly the right example to do the
jQuery/Select2 JavaScript to CoffeeScript mapping but I did find a [reverse
compiler][1] which helped.

In case it helps, I was trying to convert a working Javascript solution
(derived from the [Select2 documentation][2]):

* * *


    function personFormatResult(person) {
        var markup = "<table class=person-result><tr>"
        if (person.email !== undefined ) {
            markup += "<td>" + person.email + "</td>";
        }
        if (person.name != undefined ) {
            markup += "<td>" + person.name + "</td>";
        }
        markup += "</td></tr></table>";
        return markup;
    }

    function personFormatSelection(person) {
        var t = person.name;
        if ( person.email != "" ) {
          t += " &lt;" + person.email + "&gt;";
        }
        return t;
    }

    // presently hacked in section_id of 1

    $(document).ready(function() {
        $("#demo1").select2({
            placeholder: {name: "Search for attendee by email", email: ""},
            minimumInputLength: 1,
            ajax: {
                processData: true,
                data: function (term, page) {
                    return {
                        email: term,
                        section_id: 1
                    };
                },
                url: "/attendees/match",
                dataType: json,
                results: function (data, page) {
                    return {results: data};
                }
            },
            formatResult: personFormatResult,
            formatSelection:personFormatSelection
    })});

* * *

to CoffeeScript. One translation is

* * *

    personFormatResult = (person) ->
      markup = "<table class=person-result><tr>"
      markup += "<td>#{person.email}</td>" if person.email != undefined
      markup += "<td>#{person.name}</td>" if person.name != undefined
      markup += "</td></tr></table>"

    personFormatSelection = (person) ->
      markup = person.name
      markup +=  " &lt;" + person.email + "&gt;" if person.email != ""

    # And with the help of http://js2cs.nodejitsu.com/ (blank lines optional):

    $(document).ready ->
      $("#demo1").select2
        placeholder:
          name: "Search for attendee by email"
          email: ""

        minimumInputLength: 1

        ajax:
          processData: true

          data: (term, page) ->
            email: term
            section_id: 1

          url: "/attendees/match"

          dataType: "json"

          results: (data, page) ->
            results: data

        formatResult: personFormatResult
        formatSelection: personFormatSelection


* * *

Hope this is useful to someone else.

[1]: http://js2cs.nodejitsu.com/
[2]: http://ivaynberg.github.com/select2/


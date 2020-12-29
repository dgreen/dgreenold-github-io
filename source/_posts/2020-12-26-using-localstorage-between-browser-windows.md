---
layout: post
title: "Using localstorage between Browser Windows"
date: 2020-12-26 16:10
comments: true
categories:
---


## Overview

There are several ways to communicate between browser windows

- Server conversation (async, network delays)
- `localstorage` (sync)
- `BroadcastChannel` (most modern, does not appear to be supported in Safari)
- `IndexedDB` (async)

It looks like `localstorage` will do for the current application’s purposes of launching another window to do some work and then report back a limited amount of information and closing.

## Structure

The remote client window uses `localstorage.setItem(key,value)` to talk back to main window.  Both `key` and `value` must be strings.  `JSON.stringify(object)` may help.

Main window uses `window.addEventListener("storage", storageEventHandler, false)` to register the function `storageEventHandler(evt)` to be notified when the storage is modified.  The main window can then examine `evt.key` to get the key of the item in local storage that changed and `evt.newValue` to get the new value of the changed item.  Alternately, if only one key is in involved, the main window can use `localStorage.getItem(key)`.

## Demo Code

The demo must run in a server context not file:// and the browser windows should not be in “private” mode.

### Simulation of main window (launch this, then hit “read” link to launch client)

```
<body>
  <h1>Web localStorage (read)</h1>
  <p><a href="client.html" target="_blank">Load Client</a></p>
  <h1><span id='theString'></span></h1>
</body>

<script src="scriptRead.js"></script>

```

Body of HTML page

```
"use strict";

window.addEventListener("storage", storageEventHandler, false);
const answerFieldSpan = document.getElementById("theString");

function storageEventHandler(evt) {
  // let theString = localStorage.getItem("theString");
  // answerFieldSpan.innerText = theString;

  answerFieldSpan.innerText = `${evt.key} : ${evt.newValue}`;
}
```

JavaScript

### Simulation of client window (launched by main window or manually)

```
<body>
	<h1>Graphic Page Writing Back via Local Storage</h1>
	<form action=""></form>
	<label for="the-string">String to store:</label>
	<input type="text" name="saveValue" id="the-string">
	<button id='save'>Save</button>
</body>

<script src="scriptSet.js"></script>
```

Body of HTML page

```
"use strict";

let theString = "stop";
let check;

const saveButton = document.getElementById("save");
const theStringField = document.getElementById("the-string");

saveButton.onclick = (ev) => {
  theString = theStringField.value;
  localStorage.setItem("theString", theString);
  check = localStorage.getItem("theString");
};
```

JavaScript

## References

- [HTML Standard](https://html.spec.whatwg.org/multipage/webstorage.html) (webstorage)
- [How To Use LocalStorage to Store Data in the Browser - The Web Dev](https://thewebdev.info/2020/04/03/use-localstorage-to-store-data-on-the-browser/)
- [Storage for the web](https://web.dev/storage-for-the-web/)
- [Why using localStorage directly is a bad idea - Michal Zalecki](https://michalzalecki.com/why-using-localStorage-directly-is-a-bad-idea/)
- [How to use iOS Safari localStorage and sessionStorage in Private Mode - JonathanMH](https://jonathanmh.com/use-ios-safari-localstorage-sessionstorage-private-mode/)
- [Broadcast Channel API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API)
- [Communication between tabs or windows - Stack Overflow](https://stackoverflow.com/questions/28230845/communication-between-tabs-or-windows)


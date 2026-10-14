# readme

This example shows how to use Node.js and Express.js to exchange data between client and server in a RESTful way.

## Overview

* The client is `index.html`. It has one user-editable field (username) and two buttons:
  * one to get the username from the server
  * one to submit the username to the server
* The server is `index.js`. It maintains a variable `clientName` and exposes endpoints that let the client read or update that value.
* `index.html` uses [zepto.js](http://zeptojs.com/) (a lightweight jQuery) to make AJAX requests.
* The server serves a static `/js` directory so `index.html` can load `zepto.js` (and other static files).

{% stepper %}
{% step %}
### Installation

* Download all the components (client and server files) into one directory.
* From that directory, run:

```bash
npm install
```

This installs the project's dependencies.
{% endstep %}

{% step %}
### Server endpoints (behavior)

The server (`index.js`) provides these response functions:

* GET /\
  Serves the `index.html` page.
* GET /index\*\
  Serves `index.html` for any request that starts with `index`.
* GET /name\
  Sends the client the current value of the server variable `clientName`.
* POST /name/:name\
  Sets `clientName` to the value of `:name`.
{% endstep %}

{% step %}
### Client behavior (index.html)

* Has a text input field named `username`.
* Two buttons:
  * one button sends a GET request to retrieve the current `clientName` and fills the input field with the response
  * the other button sends a POST request with the new username to update the server-side `clientName`
* Uses zepto.js to perform the AJAX requests.
{% endstep %}

{% step %}
### Important note about static files

{% hint style="info" %}
Because `index.html` needs to load `zepto.js`, the server defines a `/js` directory to serve static files. Without that the index page won't be able to load `zepto.js` (or any other client-side files).
{% endhint %}
{% endstep %}
{% endstepper %}

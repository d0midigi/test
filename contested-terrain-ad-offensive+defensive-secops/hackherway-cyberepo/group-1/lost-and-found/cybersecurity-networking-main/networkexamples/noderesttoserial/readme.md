# README

This example allows you to send messages to an Arduino microcontroller from a web page using a RESTian communications scheme. The server application is written in node.js using the express.js web framework and node-serialport for serial communications.

{% hint style="info" %}
Make sure you have read up on [node.js](/broken/pages/da8e9b36153e1b57d2890791949c495404cb8d7c) and have it installed before proceeding.
{% endhint %}

{% stepper %}
{% step %}
### Get the project

* Either clone the project from its repository or download it and extract it.
* Change directories to the project folder from a command line / terminal.
{% endstep %}

{% step %}
### Install dependencies

Enter the following command in the project directory:

{% code title="Install dependencies" %}
```bash
npm install
```
{% endcode %}

This will create a `node_modules` directory containing the required packages, such as socket.io, node-serialport, and express.js.
{% endstep %}

{% step %}
### Run the server

Start the server with:

{% code title="Start server" %}
```bash
node restToSerial.js portname
```
{% endcode %}

Replace `portname` with the name of your serial port.
{% endstep %}
{% endstepper %}

# README

A serial-to-web example using node.js, node-serialport, and socket.io. This example converts a serial string into a JSON object and sends that via webSocket.

To use this, you should read up on [node.js](/broken/pages/da8e9b36153e1b57d2890791949c495404cb8d7c)

{% stepper %}
{% step %}
### Prerequisites

* make sure you've installed node.js
* either clone the project in git or download it
* from the command line, change directories to the directory where you downloaded the project
{% endstep %}

{% step %}
### Install dependencies

Enter the following:

```bash
npm install
```

You should end up with a new directory called `node_modules`, which will include `socket.io`, `node-serialport`, and `express.js`.
{% endstep %}

{% step %}
### Run the example

To run it, enter:

```bash
node SerialToJSON.js portname
```

Where `portname` is the name of your serial port.
{% endstep %}
{% endstepper %}

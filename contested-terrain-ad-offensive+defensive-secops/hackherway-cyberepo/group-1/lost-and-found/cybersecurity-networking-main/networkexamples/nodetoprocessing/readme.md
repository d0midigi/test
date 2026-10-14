# README

A serial-to-node-to-Processing example using node.js and node-serialport.

To use this, you should read up on [node.js](/broken/pages/da8e9b36153e1b57d2890791949c495404cb8d7c).

{% stepper %}
{% step %}
### Install the project dependencies

* Make sure you've installed node.js.
* Either clone the project in git or download it.
* From the command line, change directories to the directory where you downloaded the project.

Run:

{% code title="Install dependencies" %}
```bash
npm install
```
{% endcode %}

You should end up with a new directory called `node_modules`, which will include `socket.io`, `node-serialport`, and `express.js`.
{% endstep %}

{% step %}
### Prepare the Arduino

Install `ADXL326.ino` onto an Arduino Uno, Leonardo, or Mega that has an ADXL326 accelerometer breakout board from Adafruit attached.
{% endstep %}

{% step %}
### Run the server

From the project directory run:

{% code title="Start server" %}
```bash
node nodeToProcessing.js
```
{% endcode %}
{% endstep %}

{% step %}
### Run the Processing sketch

Open `jsonProcessing.pde` in Processing 2.0 or later, and run it. You should get a scatter graph of the X and Y coordinates from the accelerometer.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Keep the original files (`nodeToProcessing.js`, `ADXL326.ino`, and `jsonProcessing.pde`) together in the project folder so paths and serial/port settings remain correct.
{% endhint %}

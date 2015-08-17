# Install the ESP8266 core

We need the ESP8266 core to let us build our own firmwares.

## Instructions

[Follow the instructions here](https://github.com/esp8266/Arduino#installing-with-boards-manager)

# Blink

The 'hello world' of loading our own firmware. We'll use a simple example program to flash an LED connected to the ESP8266.

## Instructions

Build the circuit shown below

![led](led.png)

Load the blink example sketch and change all references to pin 13 to pin 2

In the Arduino IDE, set:

* tools->board = generic ESP8266
* tools->upload speed = 921600

Press the Upload button and also press the button on the ESP8266 board

## Advanced tasks

* Flash a more complicated pattern
* Add a button

# Remote controlled blink

We'll install a pair of libraries that add [REST](http://arest.io/) functionality to the ESP8266. Then we'll use a browser or a phone to control the LED we connected earlier.

## Instructions

Install 2 libraries:

* [aREST_UI](https://github.com/marcoschwartz/aREST_UI)
* [aREST](https://github.com/marcoschwartz/aREST)

Load example aREST UI->ESP8266

Change WIFI parameters (SSID & Password)

Change reference to pin 5 (line 36) to pin 2.

Upload (press button on PCB as well)

Open serial port and make a note of the IP address

Navigate to the IP address using a web browser

Control the LED by clicking the buttons

## Advanced tasks

* Add an extra LED
* Use the slider control to control LED brightness

# Data logging with Sparkfun

Now we'll look at logging data to a remote data store. To start with we'll just log how long the ESP8266 has been running.

## Instructions

Navigate to [data.sparkfun.com](https://data.sparkfun.com/streams/make)

Fill in the blanks (use 'value' for fields)

Press 'save' and download the keys as a json file

In Arduino IDE, load example ESP8266Wifi->WifiClient

Change WIFI parameters (SSID & Password)

Change streamId & privateKey to your details (in the json file)

Upload (press button on PCB as well)

Open serial port and watch as data is posted.

## Advanced tasks

* log button clicks or a temperature sensor
* [Graph the data](http://phant.io/graphing/google/2014/07/07/graphing-data/) with google charts.


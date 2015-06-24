# esp8266 notes

## Uploading new firmware

Followed this guide from [makezine](http://makezine.com/2015/04/01/installing-building-arduino-sketch-5-microcontroller/)

* download arduino ide extension: https://github.com/esp8266/Arduino/releases
* install into ~/sketchbook/hardware/esp8266
* select generic esp8266 as board in the ide

Necessary to pulldown gpio0 to gnd before uploading, and I needed to pull power before uploading a new sketch.

I connected led to GPIO2 and used pin 2 to flash it with blink. Works!

Sketch will start running immediately, but if power is pulled, will be wiped. So disconnect gpio0 to gnd before removing power.

I also tested the sparkfun client demo, by setting up a [data stream](https://data.sparkfun.com/streams/o8oj3Z4ZD0t5NmG5zpmn). [JSON key file](keys.json).

Followed [this example](http://phant.io/graphing/google/2014/07/07/graphing-data/) to create an [html graph](graph.html)

## Setup and first testing: Wed Jun 24 19:30:07 BST 2015

Modules arrived today. Started with simple AT serial testing.

Module [needs up to 200ma](http://wiki.iteadstudio.com/ESP8266_Serial_WIFI_Module)

Used rfduino programmer socket as at 3.3v and can provide up to 500mA.

Followed a useful [guide from rancidbacon.com](http://rancidbacon.com/files/kiwicon8/ESP8266_WiFi_Module_Quick_Start_Guide_v_1.0.4.pdf)

Did the wiring as shown in the doc. Didn't explain CH_PD, but [this pinout did](http://www.espruino.com/ESP8266). Needs to be wired to +3.3v to enable wifi.

Didn't use screen as couldn't get \n\r to work so used

    miniterm.py /dev/ttyUSB0 115200

Tested the AT commands, listed, joined wifi networks. Ran TCPserver and connected with nc.

## 19 Jun - bought modules

£7 for 2 from ebay. Etang shop.

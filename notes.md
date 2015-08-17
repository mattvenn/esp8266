# ESP8266 notes

## Writing new firmware with Arduino

* [install instructions here](https://github.com/esp8266/Arduino#installing-with-boards-manager)

Necessary to pulldown gpio0 to gnd before uploading

## Standalone mode (with switch inaccessible)

When installed into a project, the button that puts the ESP into upload mode is
not available.

[Sparkfun's
Thing](https://cdn.sparkfun.com/datasheets/Wireless/WiFi/SparkFun_ESP8266_Thing.pdf)
uses a diode between DTR and gpio0 so that when programming the pin goes low. I
couldn't get it to work.

## Low power

[Good writeup by Sparkfun](https://www.sparkfun.com/news/1842)

* arduino lib [supports this](https://github.com/esp8266/Arduino/blob/c6e2a290d1ec945c93b7571df166f0c83e1a6b49/hardware/esp8266com/esp8266/doc/reference.md#esp-specific-apis)
* gpio16 tied to reset to wakeup

With reg connected couldn't get lower than 5mA. disconnected reg got 80ma for connect/send and 18uA for deep sleep. 

18ua higher(? check this) than expected due to added resistors? eg on reset pin

Can't upload with gpio16 connected to reset. worked with a power cycle

## Boot modes

[This](http://www.esp8266.com/viewtopic.php?f=13&t=1730) explains that gpio0 & 2
both need to be high (or floating) for a normal boot. So with a sensor like the
dust sensor connected on gpio2, it will often not boot.


## Sparkfun data logging

Tested the (arduino) sparkfun client demo (wificlient), by setting up a [data stream](https://data.sparkfun.com/streams/o8oj3Z4ZD0t5NmG5zpmn).

Followed [this example](http://phant.io/graphing/google/2014/07/07/graphing-data/) to create an [html graph](graph.html)

## Other ESPs

2 GPIO pins is pretty limiting, so apart from very simple projects, the esp8266
would require another microcontroller.

There are [more
though](http://l0l.org.uk/2014/12/esp8266-modules-hardware-guide-gotta-catch-em-all/),
including the [esp03](http://esp8266.co.uk/modules/esp-03/) which has 7gpios
plus serial. 4 of the gpios can be used for SPI master.

I've ended up using the esp12 on [my breakout](https://github.com/mattvenn/kicad/tree/master/esp8266-12-breakout-smt) which seems to have the best capabilities.

## Uploading any firmware

Use [esptool](https://github.com/themadinventor/esptool), for example to load AT firmware:

./esptool.py --port /dev/ttyUSB1 --baud 921600 write_flash 0x00000 v0.9.2.2\ AT\ Firmware.bin

## AT commands (using AT firmware)

Used miniterm (but arduino serial and screen work too)

    miniterm.py /dev/ttyUSB0 115200

### list available networks

    AT+CWMODE=3
    AT+CWLAP

### join & print details

    AT+CWJAP="MRB2015","9639045620"
    AT+CIFSR

### multi connections allowed, and listen on 8000

    AT+CIPMUX=1
    AT+CIPSERVER=1,8000

### send 8 chars

    AT+CIPSEND=0,8

### connect to mattvenn.net on 40000

    AT+CIPSTART=4,"TCP","77.73.6.229",40000

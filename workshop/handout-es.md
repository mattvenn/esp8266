# Documentacion del taller

link para esta documentacion es http://ven.nz/esp-workshop

# Instalar el ESP8266 core

Necesitamos el ESP8266 core para construir neustros firmwares. [Documentacion
para functionalidad](https://github.com/esp8266/Arduino/blob/esp8266/hardware/esp8266com/esp8266/doc/reference.md)

## Instrucciones

[Sequir las instrucciones aqui](https://github.com/esp8266/Arduino#installing-with-boards-manager)

# experimentacion AT

Los primeras placas ESP fueron usadas solo para interace WIFI con un
microcontolador.

Para configurar el ESP, se usan commandos AT de forma similar para a los modulos
GPS o GSM.

## Instrucciones

Montar el circuito de abajo:

* LED +ve a pin 04
* LED -ve via resistencia a masa
* La linea 5v de USB se connecta con el regulador porque la regulador del chip
 FTDI no es feurte

![led](led-es.png)

En el IDE Arduino, activa el monitor serial y proba los commandos de abajo:

### Lista de redes disponibles

    AT+CWMODE=3
    AT+CWLAP

### Unirse y mostrar detalles

    AT+CWJAP="SSID","PASSWORD"
    AT+CIFSR

### Conectado a mattvenn.net puerto 40000

    AT+CIPSTART=4,"TCP","77.73.6.229",40000

# Parpadear

El programa el 'hola mundo'. Programaremos un ejemplo para parapadear un LED connectado con el ESP8266.

## Instructions

Cargar el ejemplo blink y cambia todos las referencias al pin 13 a pin 5.

El LED se conecta al pin 4 porque modulo ESP-12 cambio los pins 4 y 5 despues de
que la PCBs fuera diseñada.

En el IDE Arduino, cambia:

* tools->board = generic ESP8266
* tools->upload speed = 921600

Pulsar el boton 'Upload' y a la vez pulsar el boton en la placa.

## Tareas advanzados

* Parapadear una sequencia mas complicado
* Añade un buton
* Utiliza el ADC (voltaje maximo 1v)

# Remote controlled blink

We'll install a pair of libraries that add [REST](http://arest.io/) functionality to the ESP8266. Then we'll use a browser or a phone to control the LED we connected earlier.

## Instructions

[Install the libraries](https://www.arduino.cc/en/Guide/Libraries#toc4):

* [aREST_UI](https://github.com/marcoschwartz/aREST_UI/archive/master.zip)
* [aREST](https://github.com/marcoschwartz/aREST/archive/master.zip)

Load example aREST UI->ESP8266

Change WIFI parameters (SSID & Password)

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

# Deep Sleep

In deep sleep, the ESP can use 18uA or less. GPIO16 needs to be connected to
reset. My breakout board uses more than that because of the regulator.

## Instructions

To put the ESP to deepsleep mode:

    [ESP.deepSleep(microseconds, mode)](https://github.com/esp8266/Arduino/blob/esp8266/hardware/esp8266com/esp8266/doc/reference.md#esp-specific-apis)


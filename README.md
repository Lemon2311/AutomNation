# IoTFleet.js

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Overview
The IoTFleet.js library is a versatile tool that enables you to control multiple ESP32 devices from a PC remotely using JavaScript. This library is built with Bun and C++ and utilizes the EspAsyncWebServer library for seamless communication between ESP32 devices and a PC onto which the JS library is used.

## Features
- Control multiple ESP32 devices from a PC using HTTP requests and JavaScript, but the functionality is abstracted so it works like magic almost...
- Easy integration with JS libraries like the ones from npm
- The esp32 c++ async restfull API can be used with any language, and actively supports digital/analog IO
- There is also a ui located inside the ui folder that ca be used to control digital/analog IO
- The js library itself activelly supports digital output, but support for digital input and analog IO will be up asap

## Software Requirements
* Bun
* Platform.io

## How to use
First, download the project by pressing `<>Code` followed by `Download Zip`.

![Download Zip](https://github.com/Lemon2311/IoTFleet.js/assets/63803133/b0d0e1da-d7d6-4f7c-a26b-e707ec1ee5ee)

Extract the file (using a tool like WinRAR) and then:

Create a `WiFiCredentials.h` file inside `Esp32Code/src` containing your wifi credentials like so:

```cpp
// WiFiCredentials.h
const char *ssid = "YOUR-WIFI-SSID";
const char *password = "YOUR-WIFI-PASSWORD";
```

Upload the `main.cpp` file located inside `Esp32Code/src` to the ESP32 using Platform.io and view the serial monitor. After the code has uploaded and the ESP32 connected to the WiFi, the IP address of the ESP32 will appear in the serial monitor. Copy it as you'll need it in future steps.

* Note: To make sure Platform.io recognises the project, make sure to open `Esp32Code` (the ESP32 project) in a separate window.

Then using the library is easy. Create your js files inside the `bunJslib` folder and import the output function from `index.js` and use it like so:

```js
//this example is taken from use.js

import { output, input } from "./index.js";

const { d13, a27 } = output("192.168.1.138", "d13", "a27");

d13.set("high");
a27.set(2);

const { d3, a34 } = input("192.168.1.138", "d3", "a34");

d3.get();
a34.get();

```

* Note: This example sets pin d13 to high, a27 to 2V, and gets the values from d3 and a34(a=analog,d=digital). Analog voltage has a margin of arround 0.1V sometimes even 0.15V, as the function of bit value driven analog voltage pins isn`t liniar.

Then running your app is as easy as calling the following command in a terminal:

```
bun fileName.js //use the name of the file you want to use
```

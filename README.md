## WebServer_ESP32_SC_W5500 Library

[![arduino-library-badge](https://www.ardu-badge.com/badge/WebServer_ESP32_SC_W5500.svg?)](https://www.ardu-badge.com/WebServer_ESP32_SC_W5500)
[![GitHub release](https://img.shields.io/github/release/khoih-prog/WebServer_ESP32_SC_W5500.svg)](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/releases)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](#Contributing)
[![GitHub issues](https://img.shields.io/github/issues/khoih-prog/WebServer_ESP32_SC_W5500.svg)](http://github.com/khoih-prog/WebServer_ESP32_SC_W5500/issues)


<a href="https://www.buymeacoffee.com/khoihprog6" title="Donate to my libraries using BuyMeACoffee"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Donate to my libraries using BuyMeACoffee" style="height: 50px !important;width: 181px !important;" ></a>
<a href="https://www.buymeacoffee.com/khoihprog6" title="Donate to my libraries using BuyMeACoffee"><img src="https://img.shields.io/badge/buy%20me%20a%20coffee-donate-orange.svg?logo=buy-me-a-coffee&logoColor=FFDD00" style="height: 20px !important;width: 200px !important;" ></a>

---
---

## Table of Contents

* [Why do we need this WebServer_ESP32_SC_W5500 library](#why-do-we-need-this-WebServer_ESP32_SC_W5500-library)
  * [Features](#features)
  * [Sibling libraries](#Sibling-libraries)
  * [Currently supported Boards](#currently-supported-boards)
* [Changelog](changelog.md)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
  * [Use Arduino Library Manager](#use-arduino-library-manager)
  * [Manual Install](#manual-install)
  * [VS Code & PlatformIO](#vs-code--platformio)
* [Libraries' Patches](#libraries-patches)
  * [1. For fixing ESP32 compile error](#1-for-fixing-esp32-compile-error)
* [HOWTO Fix `Multiple Definitions` Linker Error](#howto-fix-multiple-definitions-linker-error)
* [HOWTO Use analogRead() with ESP32 running WiFi and/or BlueTooth (BT/BLE)](#howto-use-analogread-with-esp32-running-wifi-andor-bluetooth-btble)
  * [1. ESP32 has 2 ADCs, named ADC1 and ADC2](#1--esp32-has-2-adcs-named-adc1-and-adc2)
  * [2. ESP32 ADCs functions](#2-esp32-adcs-functions)
  * [3. ESP32 WiFi uses ADC2 for WiFi functions](#3-esp32-wifi-uses-adc2-for-wifi-functions)
* [Usage](#usage)
  * [Class Constructor](#class-constructor)
  * [Basic Operation](#basic-operations)
  * [Advanced Options](#advanced-options)
  * [Other Function Calls](#other-function-calls)
* [How to connect W5500 to ESP32_S2/S3/C3](#How-to-connect-W5500-to-ESP32_S2S3C3)
* [Examples](#examples)
  * [Original Examples](#original-examples)
    * [ 1. AdvancedWebServer](examples/AdvancedWebServer)
    * [ 2. HelloServer](examples/HelloServer)
    * [ 3. HelloServer2](examples/HelloServer2)
    * [ 4. HttpBasicAuth](examples/HttpBasicAuth)
    * [ 5. **MQTTClient_Auth**](examples/MQTTClient_Auth)
    * [ 6. **MQTTClient_Basic**](examples/MQTTClient_Basic)
    * [ 7. **MQTT_ThingStream**](examples/MQTT_ThingStream)
    * [ 8. PostServer](examples/PostServer)
    * [ 9. SimpleAuthentication](examples/SimpleAuthentication)
    * [10. UdpNTPClient](examples/UdpNTPClient)
    * [11. UdpSendReceive](examples/UdpSendReceive)
    * [12. WebClient](examples/WebClient)
    * [13. WebClientRepeating](examples/WebClientRepeating)
    * [14. WebServer](examples/WebServer)
    * [15. **multiFileProject**](examples/multiFileProject)
* [Example AdvancedWebServer](#example-advancedwebserver)
  * [File AdvancedWebServer.ino](#file-advancedwebserverino)
* [Debug Terminal Output Samples](#debug-terminal-output-samples)
  * [ 1. AdvancedWebServer on ESP32S3_DEV with ESP32_S3_W5500](#1-AdvancedWebServer-on-ESP32S3_DEV-with-ESP32_S3_W5500)
  * [ 2. MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500](#2-MQTT_ThingStream-on-ESP32S3_DEV-with-ESP32_S3_W5500)
  * [ 3. MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500](#3-MQTTClient_Auth-on-ESP32S3_DEV-with-ESP32_S3_W5500)
  * [ 4. MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500](#4-MQTTClient_Basic-on-ESP32S3_DEV-with-ESP32_S3_W5500)
  * [ 5. WebClient on ESP32S3_DEV with ESP32_S3_W5500](#5-WebClient-on-ESP32S3_DEV-with-ESP32_S3_W5500)
  * [ 6. UDPSendReceive on ESP32S3_DEV with ESP32_S3_W5500](#6-UDPSendReceive-on-ESP32S3_DEV-with-ESP32_S3_W5500)
  * [ 7. AdvancedWebServer on ESP32S2_DEV with ESP32_S2_W5500](#7-AdvancedWebServer-on-ESP32S2_DEV-with-ESP32_S2_W5500)
  * [ 8. AdvancedWebServer on ESP32C3_DEV with ESP32_C3_W5500](#8-AdvancedWebServer-on-ESP32C3_DEV-with-ESP32_C3_W5500)
* [Debug](#debug)
* [Troubleshooting](#troubleshooting)
* [Releases](#releases)
* [Issues](#issues)
* [TO DO](#to-do)
* [DONE](#done)
* [Contributions and Thanks](#contributions-and-thanks)
* [Contributing](#contributing)
* [License](#license)
* [Copyright](#copyright)


---
---

### Why do we need this [WebServer_ESP32_SC_W5500 library](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500)

#### Features

This [**WebServer_ESP32_SC_W5500 library**](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500) is a simple yet complete WebServer wrapper library for **ESP32_S2/S3/C3-based** boards using `LwIP W5500 Ethernet`. The functions are similar and compatible to those of [`ESP32 WebServer`](https://github.com/espressif/arduino-esp32/tree/master/libraries/WebServer) and [`ESP8266WebServer`](https://github.com/esp8266/Arduino/tree/master/libraries/ESP8266WebServer) libraries to make life much easier to port sketches from ESP8266/ESP32.

This [**WebServer_ESP32_SC_W5500 library**](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500) also provides high-level **HTTP(S), MQTT(S) and WebSockets Client** by using the functions from ESP32's [**HTTPClient Library**](https://github.com/espressif/arduino-esp32/tree/master/libraries/HTTPClient)

The library provides these features:

1. TCP Server and Client
2. UDP Server and Client
3. HTTP(S) Server and Client
4. HTTP(S) GET and POST requests, provides argument parsing, handles one client at a time.
5. **High-level HTTP(S) (GET, POST, PUT, PATCH, DELETE), MQTT(S) and WebSocket Client**.

Library is providing similar functions to:

1. [Ivan Grokhotkov's ESP32 WebServer](https://github.com/espressif/arduino-esp32/tree/master/libraries/WebServer)
2. [HTTPClient Library](https://github.com/espressif/arduino-esp32/tree/master/libraries/HTTPClient)



---

#### Sibling libraries

Please also check these sibling libraries

1. [WebServer_WT32_ETH01](https://github.com/khoih-prog/WebServer_WT32_ETH01) for ESP32-based `WT32_ETH01` using `LwIP LAN8720`
2. [WebServer_ESP32_ENC](https://github.com/khoih-prog/WebServer_ESP32_ENC) for ESP32-boards using `LwIP ENC28J60`
3. [WebServer_ESP32_W5500](https://github.com/khoih-prog/WebServer_ESP32_W5500) for ESP32-boards using `LwIP W5500`
4. [WebServer_ESP32_W6100](https://github.com/khoih-prog/WebServer_ESP32_W6100) for ESP32-boards using `LwIP W6100`
5. [WebServer_ESP32_SC_ENC](https://github.com/khoih-prog/WebServer_ESP32_SC_ENC) for ESP32_S3-boards using `LwIP ENC28J60`
6. [WebServer_ESP32_SC_W5500](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500) for ESP32_S3-boards using `LwIP W5500`
7. [WebServer_ESP32_SC_W6100](https://github.com/khoih-prog/WebServer_ESP32_SC_W6100) for ESP32_S3-boards using `LwIP W6100`

and more complex libraries for ESP32-based using `LwIP Ethernet`

#### General Libraries

 1. [AsyncHTTPRequest_ESP32_Ethernet](https://github.com/khoih-prog/AsyncHTTPRequest_ESP32_Ethernet)
 2. [AsyncHTTPSRequest_ESP32_Ethernet](https://github.com/khoih-prog/AsyncHTTPSRequest_ESP32_Ethernet)
 3. [AsyncMQTT_ESP32](https://github.com/khoih-prog/AsyncMQTT_ESP32)
 4. [HTTPS_Server_Generic](https://github.com/khoih-prog/HTTPS_Server_Generic)
 
#### ESP32_Ethernet_Manager Libraries
 
 1. [ESP32_ENC_Manager](https://github.com/khoih-prog/ESP32_ENC_Manager)
 2. [ESP32_W5500_Manager](https://github.com/khoih-prog/ESP32_W5500_Manager)
 3. [ESP32_Ethernet_Manager](https://github.com/khoih-prog/ESP32_Ethernet_Manager)
 4. [ESP32_SC_ENC_Manager](https://github.com/khoih-prog/ESP32_SC_ENC_Manager)
 5. [ESP32_SC_W5500_Manager](https://github.com/khoih-prog/ESP32_SC_W5500_Manager)
 6. [ESP32_SC_Ethernet_Manager](https://github.com/khoih-prog/ESP32_SC_Ethernet_Manager)
 
#### AsyncESP32_Ethernet_Manager Libraries
 
 1. [AsyncESP32_ENC_Manager](https://github.com/khoih-prog/AsyncESP32_ENC_Manager)
 2. [AsyncESP32_W5500_Manager](https://github.com/khoih-prog/AsyncESP32_W5500_Manager)
 3. [AsyncESP32_Ethernet_Manager](https://github.com/khoih-prog/AsyncESP32_Ethernet_Manager)
 4. [AsyncESP32_SC_ENC_Manager](https://github.com/khoih-prog/AsyncESP32_SC_ENC_Manager)
 5. [AsyncESP32_SC_W5500_Manager](https://github.com/khoih-prog/AsyncESP32_SC_W5500_Manager)
 6. [AsyncESP32_SC_Ethernet_Manager](https://github.com/khoih-prog/AsyncESP32_SC_Ethernet_Manager)
 
#### AsyncUDP_ESP32 Libraries
 
 1. [AsyncUDP_ESP32_ENC](https://github.com/khoih-prog/AsyncUDP_ESP32_ENC)
 2. [AsyncUDP_ESP32_W5500](https://github.com/khoih-prog/AsyncUDP_ESP32_W5500)
 3. [AsyncUDP_ESP32_W6100](https://github.com/khoih-prog/AsyncUDP_ESP32_W6100)
 4. [AsyncUDP_ESP32_Ethernet](https://github.com/khoih-prog/AsyncUDP_ESP32_Ethernet)
 5. [AsyncUDP_ESP32_SC_ENC](https://github.com/khoih-prog/AsyncUDP_ESP32_SC_ENC)
 6. [AsyncUDP_ESP32_SC_W5500](https://github.com/khoih-prog/AsyncUDP_ESP32_SC_W5500)
 7. [AsyncUDP_ESP32_SC_W6100](https://github.com/khoih-prog/AsyncUDP_ESP32_SC_W6100)
 8. [AsyncUDP_ESP32_SC_Ethernet](https://github.com/khoih-prog/AsyncUDP_ESP32_SC_Ethernet)

#### AsyncDNSServer_ESP32 Libraries

 1. [AsyncDNSServer_ESP32_ENC](https://github.com/khoih-prog/AsyncDNSServer_ESP32_ENC)
 2. [AsyncDNSServer_ESP32_W5500](https://github.com/khoih-prog/AsyncDNSServer_ESP32_W5500)
 3. [AsyncDNSServer_ESP32_W6100](https://github.com/khoih-prog/AsyncDNSServer_ESP32_W6100)
 4. [AsyncDNSServer_ESP32_Ethernet](https://github.com/khoih-prog/AsyncDNSServer_ESP32_Ethernet)


---


#### Currently supported Boards

This [**WebServer_ESP32_SC_W5500** library](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500) currently supports these following boards:

 1. **ESP32_S3 boards** using `LwIP W5500 Ethernet`
 2. **ESP32_S2 boards** using `LwIP W5500 Ethernet`
 3. **ESP32_C3 boards** using `LwIP W5500 Ethernet`
 
---

#### ESP32S2_DEV

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/ESP32S2_DEV.png">
</p> 

#### ESP32S3_DEV

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/ESP32S3_DEV.png">
</p> 

#### ESP32C3_DEV

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/ESP32_C3_DevKitC_02.png">
</p> 

---

#### W5500

`FULL_DUPLEX, 100Mbps`

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/W5500.png">
</p>
 
<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/W5500_small.png">
</p> 
 
---
---


## Prerequisites

 1. [`Arduino IDE 1.8.19+` for Arduino](https://github.com/arduino/Arduino). [![GitHub release](https://img.shields.io/github/release/arduino/Arduino.svg)](https://github.com/arduino/Arduino/releases/latest)
 2. [`ESP32 Core 2.0.6+`](https://github.com/espressif/arduino-esp32) for ESP32-based ESP32S2/S3/C3_DEV with W5500 boards. [![Latest release](https://img.shields.io/github/release/espressif/arduino-esp32.svg)](https://github.com/espressif/arduino-esp32/releases/latest/)


---
---

## Installation

### Use Arduino Library Manager

The best and easiest way is to use `Arduino Library Manager`. Search for `WebServer_ESP32_SC_W5500`, then select / install the latest version.
You can also use this link [![arduino-library-badge](https://www.ardu-badge.com/badge/WebServer_ESP32_SC_W5500.svg?)](https://www.ardu-badge.com/WebServer_ESP32_SC_W5500) for more detailed instructions.

### Manual Install

1. Navigate to [WebServer_ESP32_SC_W5500](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500) page.
2. Download the latest release `WebServer_ESP32_SC_W5500-main.zip`.
3. Extract the zip file to `WebServer_ESP32_SC_W5500-main` directory 
4. Copy the whole `WebServer_ESP32_SC_W5500-main` folder to Arduino libraries' directory such as `~/Arduino/libraries/`.

### VS Code & PlatformIO:

1. Install [VS Code](https://code.visualstudio.com/)
2. Install [PlatformIO](https://platformio.org/platformio-ide)
3. Install [**WebServer_ESP32_SC_W5500** library](https://registry.platformio.org/libraries/khoih-prog/WebServer_ESP32_SC_W5500) by using [Library Manager](https://registry.platformio.org/libraries/khoih-prog/WebServer_ESP32_SC_W5500/installation). Search for WebServer_ESP32_SC_W5500 in [Platform.io Author's Libraries](https://platformio.org/lib/search?query=author:%22Khoi%20Hoang%22)
4. Use included [platformio.ini](platformio/platformio.ini) file from examples to ensure that all dependent libraries will installed automatically. Please visit documentation for the other options and examples at [Project Configuration File](https://docs.platformio.org/page/projectconf.html)

---
---


### Libraries' Patches

#### 1. For fixing ESP32 compile error

To fix [`ESP32 compile error`](https://github.com/espressif/arduino-esp32), just copy the following file into the [`ESP32`](https://github.com/espressif/arduino-esp32) cores/esp32 directory (e.g. ./arduino-1.8.19/hardware/espressif/cores/esp32) to overwrite the old file:
- [Server.h](LibraryPatches/esp32/cores/esp32/Server.h)


---
---


### HOWTO Fix `Multiple Definitions` Linker Error

The current library implementation, using `xyz-Impl.h` instead of standard `xyz.cpp`, possibly creates certain `Multiple Definitions` Linker error in certain use cases.

You can include this `.hpp` file

```cpp
// Can be included as many times as necessary, without `Multiple Definitions` Linker Error
#include "WebServer_ESP32_SC_W5500.hpp"     //https://github.com/khoih-prog/WebServer_ESP32_SC_W5500
```

in many files. But be sure to use the following `.h` file **in just 1 `.h`, `.cpp` or `.ino` file**, which must **not be included in any other file**, to avoid `Multiple Definitions` Linker Error

```cpp
// To be included only in main(), .ino with setup() to avoid `Multiple Definitions` Linker Error
#include "WebServer_ESP32_SC_W5500.h"           //https://github.com/khoih-prog/WebServer_ESP32_SC_W5500
```

Check the new [**multiFileProject** example](examples/multiFileProject) for a `HOWTO` demo.

---
---


### HOWTO Use analogRead() with ESP32 running WiFi and/or BlueTooth (BT/BLE)

Please have a look at [**ESP_WiFiManager Issue 39: Not able to read analog port when using the autoconnect example**](https://github.com/khoih-prog/ESP_WiFiManager/issues/39) to have more detailed description and solution of the issue.

#### 1.  ESP32 has 2 ADCs, named ADC1 and ADC2

#### 2. ESP32 ADCs functions

- `ADC1` controls ADC function for pins **GPIO32-GPIO39**
- `ADC2` controls ADC function for pins **GPIO0, 2, 4, 12-15, 25-27**

#### 3. ESP32 WiFi uses ADC2 for WiFi functions

Look in file [**adc_common.c**](https://github.com/espressif/esp-idf/blob/master/components/driver/adc_common.c#L61)

> In ADC2, there're two locks used for different cases:
> 1. lock shared with app and Wi-Fi:
>    ESP32:
>         When Wi-Fi using the ADC2, we assume it will never stop, so app checks the lock and returns immediately if failed.
>    ESP32S2:
>         The controller's control over the ADC is determined by the arbiter. There is no need to control by lock.
> 
> 2. lock shared between tasks:
>    when several tasks sharing the ADC2, we want to guarantee
>    all the requests will be handled.
>    Since conversions are short (about 31us), app returns the lock very soon,
>    we use a spinlock to stand there waiting to do conversions one by one.
> 
> adc2_spinlock should be acquired first, then adc2_wifi_lock or rtc_spinlock.


- In order to use `ADC2` for other functions, we have to **acquire complicated firmware locks and very difficult to do**
- So, it's not advisable to use `ADC2` with WiFi/BlueTooth (BT/BLE).
- Use `ADC1`, and pins GPIO32-GPIO39
- If somehow it's a must to use those pins serviced by `ADC2` (**GPIO0, 2, 4, 12, 13, 14, 15, 25, 26 and 27**), use the **fix mentioned at the end** of [**ESP_WiFiManager Issue 39: Not able to read analog port when using the autoconnect example**](https://github.com/khoih-prog/ESP_WiFiManager/issues/39) to work with ESP32 WiFi/BlueTooth (BT/BLE).


---
---

## Usage


### Class Constructor

```cpp
WebServer server(80);
```

Creates the `WebServer_ESP32_SC_W5500` class object.

**Parameters:**
 
host port number: ``int port`` (default is the standard HTTP port 80)

---

### Basic Operations

#### Starting the server

```cpp
void begin();
```

#### Handling incoming client requests

```cpp
void handleClient();
```

#### Disabling the server

```cpp
void close();
void stop();
```

Both methods function the same

#### Client request handlers

```cpp
void on();
void addHandler();
void onNotFound();
void onFileUpload();	
```

Example:

```cpp
server.on("/", handlerFunction);
server.onNotFound(handlerFunction);   // called when handler is not assigned
server.onFileUpload(handlerFunction); // handle file uploads
```

#### Sending responses to the client

```cpp
void send();
void send_P();
```

**Parameters:**

`code` - HTTP response code, can be `200` or `404`, etc.

`content_type` - HTTP content type, like `"text/plain"` or `"image/png"`, etc.

`content` - actual content body

---

### Advanced Options

#### Getting information about request arguments

```cpp
const String & arg();
const String & argName();
int args();
bool hasArg();
```

**Function usage:**

`arg` - get request argument value, use `arg("plain")` to get POST body
	
`argName` - get request argument name
	
`args` - get arguments count
	
`hasArg` - check if argument exist


#### Getting information about request headers

```cpp
const String & header();
const String & headerName();
const String & hostHeader();
int headers();
bool hasHeader();
```

**Function usage:**

`header` - get request header value

`headerName` - get request header name

`hostHeader` - get request host header if available, else empty string
  
`headers` - get header count
	
`hasHeader` - check if header exist


#### Authentication

```cpp
bool authenticate();
void requestAuthentication();
```

**Function usage:**

`authenticate` - server authentication, returns true if client is authenticated else false

`requestAuthentication` - sends authentication failure response to the client

**Example Usage:**

```cpp
if(!server.authenticate(username, password))
{
  server.requestAuthentication();
}
```

#### Other Function Calls

```cpp
const String & uri();     // get the current uri
HTTPMethod  method();     // get the current method 
WiFiClient client();      // get the current client
HTTPUpload & upload();    // get the current upload
void setContentLength();  // set content length
void sendHeader();        // send HTTP header
void sendContent();       // send content
void sendContent_P(); 
void collectHeaders();    // set the request headers to collect
void serveStatic();
size_t streamFile();
```


---
---

### How to connect W5500 to ESP32_S2/S3/C3

You can change the `INT` pin to another one. Default is `GPIO4`

```cpp
// Must connect INT to GPIOxx or not working
#define INT_GPIO            4
```

---

#### W5500

`FULL_DUPLEX, 100Mbps`

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/W5500.png">
</p>
 
<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/W5500_small.png">
</p> 
 
---


#### ESP32S3_DEV

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/ESP32S3_DEV.png">
</p> 


|W5500|<--->|ESP32_S3|
|:-:|:-:|:-:|
|MOSI|<--->|GPIO11|
|MISO|<--->|GPIO13|
|SCK|<--->|GPIO12|
|SS|<--->|GPIO10|
|INT|<--->|GPIO4|
|RST|<--->|RST|
|GND|<--->|GND|
|3.3V|<--->|3.3V|

---

#### ESP32S2_DEV

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/ESP32S2_DEV.png">
</p> 


|W5500|<--->|ESP32_S2|
|:-:|:-:|:-:|
|MOSI|<--->|GPIO35|
|MISO|<--->|GPIO37|
|SCK|<--->|GPIO36|
|SS|<--->|GPIO34|
|INT|<--->|GPIO4|
|RST|<--->|RST|
|GND|<--->|GND|
|3.3V|<--->|3.3V|

---


#### ESP32C3_DEV

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/ESP32_C3_DevKitC_02.png">
</p> 


|W5500|<--->|ESP32_C3|
|:-:|:-:|:-:|
|MOSI|<--->|GPIO6|
|MISO|<--->|GPIO5|
|SCK|<--->|GPIO4|
|SS|<--->|GPIO7|
|INT|<--->|GPIO10|
|RST|<--->|RST|
|GND|<--->|GND|
|3.3V|<--->|3.3V|


---
---

### Examples:

#### Original Examples

 1. [AdvancedWebServer](examples/AdvancedWebServer)
 2. [HelloServer](examples/HelloServer)
 3. [HelloServer2](examples/HelloServer2)
 4. [HttpBasicAuth](examples/HttpBasicAuth)
 5. [**MQTTClient_Auth**](examples/MQTTClient_Auth)
 6. [**MQTTClient_Basic**](examples/MQTTClient_Basic)
 7. [**MQTT_ThingStream**](examples/MQTT_ThingStream)
 8. [PostServer](examples/PostServer)
 9. [SimpleAuthentication](examples/SimpleAuthentication)
10. [UdpNTPClient](examples/UdpNTPClient)
11. [UdpSendReceive](examples/UdpSendReceive)
12. [WebClient](examples/WebClient)
13. [WebClientRepeating](examples/WebClientRepeating)
14. [WebServer](examples/WebServer)
15. [**multiFileProject**](examples/multiFileProject)

---
---

### Example [AdvancedWebServer](examples/AdvancedWebServer)

#### File [AdvancedWebServer.ino](examples/AdvancedWebServer/AdvancedWebServer.ino)


https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/blob/de023206ab284ab9e0cfd063316ea0946eb5eff0/examples/AdvancedWebServer/AdvancedWebServer.ino#L41-L293

---
---

### Debug Terminal Output Samples

#### 1. AdvancedWebServer on ESP32S3_DEV with ESP32_S3_W5500

The following are debug terminal output and screen shot when running example [AdvancedWebServer](examples/AdvancedWebServer) on `ESP32S3_DEV` with `ESP32_S3_W5500`

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/AdvancedWebServer.png">
</p>

```cpp
Start AdvancedWebServer on ESP32S3_DEV with ESP32_S3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 11
[EWS] MISO: 13
[EWS] SCK: 12
[EWS] CS: 10
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================

ETH Started
ETH Connected
ETH MAC: DE:AD:BE:EF:BE:0E, IPv4: 192.168.2.106
FULL_DUPLEX, 100Mbps
HTTP EthernetWebServer is @ IP : 192.168.2.106
.......... ..........
```

---

#### 2. MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500

The terminal output of **ESP32S3_DEV with W5500** running [MQTT_ThingStream example](examples/MQTT_ThingStream)


```cpp
Start MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 11
[EWS] MISO: 13
[EWS] SCK: 12
[EWS] CS: 10
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================

ETH Started
ETH Connected
ETH MAC: DE:AD:BE:EF:BE:0E, IPv4: 192.168.2.106
FULL_DUPLEX, 100Mbps
***************************************
ESP32_Pub
***************************************
MQTT Message Send : ESP32_Pub => Hello from MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500
MQTT Message receive [ESP32_Pub] Hello from MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500
MQTT Message Send : ESP32_Pub => Hello from MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500
MQTT Message receive [ESP32_Pub] Hello from MQTT_ThingStream on ESP32S3_DEV with ESP32_S3_W5500
```

---

#### 3. MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500

The terminal output of **ESP32S3_DEV with W5500** running [MQTTClient_Auth example](examples/MQTTClient_Auth)


```cpp
Start MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 11
[EWS] MISO: 13
[EWS] SCK: 12
[EWS] CS: 10
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================

ETH Started
ETH Connected
ETH MAC: DE:AD:BE:EF:BE:0E, IPv4: 192.168.2.106
FULL_DUPLEX, 100Mbps
Message Send : MQTT_Pub => Hello from MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500
Message arrived [MQTT_Pub] Hello from MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500
Message Send : MQTT_Pub => Hello from MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500
Message arrived [MQTT_Pub] Hello from MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500
Message Send : MQTT_Pub => Hello from MQTTClient_Auth on ESP32S3_DEV with ESP32_S3_W5500
```

---

#### 4. MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500

The terminal output of **ESP32S3_DEV with W5500** running [MQTTClient_Basic example](examples/MQTTClient_Basic)

```cpp
Start MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 11
[EWS] MISO: 13
[EWS] SCK: 12
[EWS] CS: 10
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================

ETH Started
ETH Connected
ETH MAC: DE:AD:BE:EF:BE:0E, IPv4: 192.168.2.106
FULL_DUPLEX, 100Mbps
Message Send : MQTT_Pub => Hello from MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500
Message arrived [MQTT_Pub] Hello from MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500
Message Send : MQTT_Pub => Hello from MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500
Message arrived [MQTT_Pub] Hello from MQTTClient_Basic on ESP32S3_DEV with ESP32_S3_W5500
```

---


#### 5. WebClient on ESP32S3_DEV with ESP32_S3_W5500

The terminal output of **ESP32S3_DEV with W5500** running [WebClient example](examples/WebClient)

```cpp
Start WebClient on ESP32S3_DEV with ESP32_S3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 11
[EWS] MISO: 13
[EWS] SCK: 12
[EWS] CS: 10
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================

ETH Started
ETH Connected
ETH MAC: DE:AD:BE:EF:BE:0A, IPv4: 192.168.2.98
FULL_DUPLEX, 100Mbps

Starting connection to server...
Connected to server
HTTP/1.1 200 OK
Date: Wed, 14 Dec 2022 05:19:00 GMT
Content-Type: text/plain
Content-Length: 2263
Connection: close
x-amz-id-2: I1XSxb8SrBbQvFZiDm6s+3yCJDQ/kr8viynhpV/gMhEc444Vesm23XUdidJIuVKxLKvyEevxZ40=
x-amz-request-id: 8TV8DXN77NW79TND
Last-Modified: Wed, 23 Feb 2022 14:56:42 GMT
ETag: "667cf48afcc12c38c8c1637947a04224"
CF-Cache-Status: DYNAMIC
Report-To: {"endpoints":[{"url":"https:\/\/a.nel.cloudflare.com\/report\/v3?s=E5WKZrRe9b85co%2BkMLkh7ffnNJ3p4%2BWsN%2BwjN6GQFwshsImPjF1CUUDDDB7aDvMmWXpdWdPqNcz104aCGcSpcSgZIRkOwJuGE5hGN3ZLxa3JtJecrpo%2FUGwZPebWKB8%3D"}],"group":"cf-nel","max_age":604800}
NEL: {"success_fraction":0,"report_to":"cf-nel","max_age":604800}
Server: cloudflare
CF-RAY: 77947b6a7a8954a9-YYZ
alt-svc: h3=":443"; ma=86400, h3-29=":443"; ma=86400


           `:;;;,`                      .:;;:.           
        .;;;;;;;;;;;`                :;;;;;;;;;;:     TM 
      `;;;;;;;;;;;;;;;`            :;;;;;;;;;;;;;;;      
     :;;;;;;;;;;;;;;;;;;         `;;;;;;;;;;;;;;;;;;     
    ;;;;;;;;;;;;;;;;;;;;;       .;;;;;;;;;;;;;;;;;;;;    
   ;;;;;;;;:`   `;;;;;;;;;     ,;;;;;;;;.`   .;;;;;;;;   
  .;;;;;;,         :;;;;;;;   .;;;;;;;          ;;;;;;;  
  ;;;;;;             ;;;;;;;  ;;;;;;,            ;;;;;;. 
 ,;;;;;               ;;;;;;.;;;;;;`              ;;;;;; 
 ;;;;;.                ;;;;;;;;;;;`      ```       ;;;;;`
 ;;;;;                  ;;;;;;;;;,       ;;;       .;;;;;
`;;;;:                  `;;;;;;;;        ;;;        ;;;;;
,;;;;`    `,,,,,,,,      ;;;;;;;      .,,;;;,,,     ;;;;;
:;;;;`    .;;;;;;;;       ;;;;;,      :;;;;;;;;     ;;;;;
:;;;;`    .;;;;;;;;      `;;;;;;      :;;;;;;;;     ;;;;;
.;;;;.                   ;;;;;;;.        ;;;        ;;;;;
 ;;;;;                  ;;;;;;;;;        ;;;        ;;;;;
 ;;;;;                 .;;;;;;;;;;       ;;;       ;;;;;,
 ;;;;;;               `;;;;;;;;;;;;                ;;;;; 
 `;;;;;,             .;;;;;; ;;;;;;;              ;;;;;; 
  ;;;;;;:           :;;;;;;.  ;;;;;;;            ;;;;;;  
   ;;;;;;;`       .;;;;;;;,    ;;;;;;;;        ;;;;;;;:  
    ;;;;;;;;;:,:;;;;;;;;;:      ;;;;;;;;;;:,;;;;;;;;;;   
    `;;;;;;;;;;;;;;;;;;;.        ;;;;;;;;;;;;;;;;;;;;    
      ;;;;;;;;;;;;;;;;;           :;;;;;;;;;;;;;;;;:     
       ,;;;;;;;;;;;;;,              ;;;;;;;;;;;;;;       
         .;;;;;;;;;`                  ,;;;;;;;;:         
                                                         
                                                         
                                                         
                                                         
    ;;;   ;;;;;`  ;;;;:  .;;  ;; ,;;;;;, ;;. `;,  ;;;;   
    ;;;   ;;:;;;  ;;;;;; .;;  ;; ,;;;;;: ;;; `;, ;;;:;;  
   ,;:;   ;;  ;;  ;;  ;; .;;  ;;   ,;,   ;;;,`;, ;;  ;;  
   ;; ;:  ;;  ;;  ;;  ;; .;;  ;;   ,;,   ;;;;`;, ;;  ;;. 
   ;: ;;  ;;;;;:  ;;  ;; .;;  ;;   ,;,   ;;`;;;, ;;  ;;` 
  ,;;;;;  ;;`;;   ;;  ;; .;;  ;;   ,;,   ;; ;;;, ;;  ;;  
  ;;  ,;, ;; .;;  ;;;;;:  ;;;;;: ,;;;;;: ;;  ;;, ;;;;;;  
  ;;   ;; ;;  ;;` ;;;;.   `;;;:  ,;;;;;, ;;  ;;,  ;;;;   

Disconnecting from server...
```

---

#### 6. UDPSendReceive on ESP32S3_DEV with ESP32_S3_W5500

The terminal output of **ESP32S3_DEV with W5500** running [UDPSendReceive example](examples/UDPSendReceive)

```cpp
Start UDPSendReceive on ESP32S3_DEV with ESP32_S3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 11
[EWS] MISO: 13
[EWS] SCK: 12
[EWS] CS: 10
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================

ETH Started
ETH Connected
ETH MAC: DE:AD:BE:EF:FE:09, IPv4: 192.168.2.94
FULL_DUPLEX, 100Mbps

Starting connection to server...
Listening on port 2390
UDP Packet received, size 48
From 132.163.97.3, port 123
Seconds since Jan 1 1900 = 3879985481
Unix time = 1670996681
The UTC time is 5:44:41
UDP Packet received, size 48
From 132.163.97.3, port 123
Seconds since Jan 1 1900 = 3879985493
Unix time = 1670996693
The UTC time is 5:44:53
UDP Packet received, size 48
From 132.163.97.3, port 123
Seconds since Jan 1 1900 = 3879985505
Unix time = 1670996705
The UTC time is 5:45:05
```

---


#### 7. AdvancedWebServer on ESP32S2_DEV with ESP32_S2_W5500

The following are debug terminal output and screen shot when running example [AdvancedWebServer](examples/AdvancedWebServer) on `ESP32S2_DEV` with `ESP32_S2_W5500`. The `built-in MAC address` is used now instead of user-defined one.

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/AdvancedWebServer_ESP32_S2.png">
</p>

```cpp
Start AdvancedWebServer on ESP32S2_DEV with ESP32_S2_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 2
[EWS] MOSI: 35
[EWS] MISO: 37
[EWS] SCK: 36
[EWS] CS: 34
[EWS] INT: 4
[EWS] SPI Clock (MHz): 25
[EWS] =========================
Using built-in mac_eth = 7E:DF:A1:08:32:C9

ETH Started
ETH Connected
ETH MAC: 7E:DF:A1:08:32:C9, IPv4: 192.168.2.133
FULL_DUPLEX, 100Mbps
HTTP EthernetWebServer is @ IP : 192.168.2.133
...
```

---


#### 8. AdvancedWebServer on ESP32C3_DEV with ESP32_C3_W5500

The following are debug terminal output and screen shot when running example [AdvancedWebServer](examples/AdvancedWebServer) on `ESP32C3_DEV` with `ESP32_C3_W5500`. The `built-in MAC address` is used now instead of user-defined one.

<p align="center">
    <img src="https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/raw/main/pics/AdvancedWebServer_ESP32_C3.png">
</p>


```cpp
Start AdvancedWebServer on ESP32C3_DEV with ESP32_C3_W5500
WebServer_ESP32_SC_W5500 v1.2.1 for core v2.0.0+
[EWS] Default SPI pinout:
[EWS] SPI_HOST: 1
[EWS] MOSI: 6
[EWS] MISO: 5
[EWS] SCK: 4
[EWS] CS: 7
[EWS] INT: 10
[EWS] SPI Clock (MHz): 25
[EWS] =========================
Using built-in mac_eth = 7C:DF:A1:BC:BC:53

ETH Started
ETH Connected
ETH MAC: 7C:DF:A1:BC:BC:53, IPv4: 192.168.2.135
FULL_DUPLEX, 100Mbps
HTTP EthernetWebServer is @ IP : 192.168.2.135
...
```

---
---

### Debug

Debug is enabled by default on Serial. Debug Level from 0 to 4. To disable, change the _ETHERNET_WEBSERVER_LOGLEVEL_ to 0

```cpp
// Use this to output debug msgs to Serial
#define DEBUG_ETHERNET_WEBSERVER_PORT       Serial
// Use this to disable all output debug msgs
// Debug Level from 0 to 4
#define _ETHERNET_WEBSERVER_LOGLEVEL_       0
```

---

## Troubleshooting

If you get compilation errors, more often than not, you may need to install a newer version of the board's core, applying Libraries' Patches, Packages' Patches or this library latest version.

---
---


### Issues ###

Submit issues to: [WebServer_ESP32_SC_W5500 issues](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/issues)

---

### TO DO

1. Bug Searching and Killing


### DONE

 1. Add support to **ESP32S3-based boards** using `LwIP W5500 Ethernet`
 2. Using `SPI_DMA_CH_AUTO` instead of manually selected
 3. Add example [multiFileProject](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/tree/main/examples/multiFileProject)
 4. Add support to **ESP32S2-based boards** using `LwIP W5500 Ethernet`
 5. Add support to **ESP32_C3-based boards** using `LwIP W5500 Ethernet`
 6. Remove unused variable to avoid compiler warning and error
 
---
---

### Contributions and Thanks


Many thanks for everyone for bug reporting, new feature suggesting, testing and contributing to the development of this library.

1. Based on the [Ivan Grokhotkov's ESP32 WebServer](https://github.com/espressif/arduino-esp32/tree/master/libraries/WebServer) and [HTTPClient Library](https://github.com/espressif/arduino-esp32/tree/master/libraries/HTTPClient) libraries
8. Thanks to [avanderhoest](https://github.com/avanderhoest) for reporting [Supporting ESP32_S3 using W5500 Ethernet #72](https://github.com/khoih-prog/EthernetWebServer/discussions/72) leading to the creation of this library


<table>
  <tr>
    <td align="center"><a href="https://github.com/igrr"><img src="https://github.com/igrr.png" width="100px;" alt="igrr"/><br /><sub><b>⭐️ Ivan Grokhotkov</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/avanderhoest"><img src="https://github.com/avanderhoest.png" width="100px;" alt="avanderhoest"/><br /><sub><b>avanderhoest</b></sub></a><br /></td>
  </tr> 
</table>

---

### Contributing

If you want to contribute to this project:
- Report bugs and errors
- Ask for enhancements
- Create issues and pull requests
- Tell other people about this library

---

### License

- The library is licensed under [GPLv3](https://github.com/khoih-prog/WebServer_ESP32_SC_W5500/blob/main/LICENSE)

---

## Copyright

- Copyright (c) 2016- Ivan Grokhotkov

- Copyright (c) 2022- Khoi Hoang



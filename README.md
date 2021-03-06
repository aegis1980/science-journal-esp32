# ESP32 talking to Arduino Science Journal App via BLE

This is nothing more than a refactoring and updating of the [code here by Uriah Welcome](https://github.com/precision/science-journal-arduino/tree/esp32) which added ESP32 as an option to the original [Science Journal Arduino repo][sj-arduino].

## What does this code do?

Let's you set up a quick and easy BLE connection between your ESP32 device and the Arduino Science Journal app ([Android](https://play.google.com/store/apps/details?id=cc.arduino.sciencejournal) and [iOS](https://apps.apple.com/us/app/arduino-science-journal/id1518014927)). Science Journal lets you graph and record data from your phone's internal sensors...and external sensors via Bluetooth.

## How do I use it?
See `examples/main.cpp`

Add the following to your `platformio.ini` (assuming you are PlatformIO...which I am with VS code):
```
lib_deps = 
    https://github.com/aegis1980/science-journal-esp32.git
```
You might also need to add the following to your `platformio.ini`:
```
board_build.partitions = min_spiffs.csv
```
Without this I run out of space when uploading firmware with the  generic ESP32 dev boards I am using.

----
## To-dos

- Work out how to tailor the characteristics of the data going between the ESP32 and app. For example there is currently an option for 'rotation' displayed in RPM which does nothing. Something to do with [`sensor.pb.h`](./src/sensor.pb.h) & [`sensor.pb.c`](./src/sensor.pb.c)
- Naming of device still uses Wifi id - original author could not rename once initialised [`Esp32BLE.h`](./src/Esp32BLE.h). See original authors comment in code ... like I said, I really contributed nothing to original code

----
## Modifications to [forked repo](https://github.com/precision/science-journal-arduino/tree/esp32):

* Updated for PlatformIO 2021 (CORE 5.x)
* Stripped out all the non-ESP32 stuff and not used code - refer to [the original repo][sj-arduino] if you need that stuff.
* Restructured things so packaged up as a [PlatformIO library](./library.json)
* Removed dependency on [`nkolban/ESP32 BLE Arduino`](https://github.com/nkolban/ESP32_BLE_Arduino) seems to run just find with BLE implementation now included in Arduino.


## License

Open Science Journal is licensed under the Apache 2 license. Refer [here][sj-arduino] and [here][sj-android] for licenses. 

Anything that does not fall under these licenses in this repo (ie anything I have added that is not derivative-or-whatever) is under the [Unlicense license](https://unlicense.org).

[sj-arduino]: https://github.com/google/science-journal-arduino
[sj-android]: https://github.com/arduino/Arduino-Science-Journal-Android

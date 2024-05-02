﻿# Enhanced Nextion Library with multi display instance support

Jyrki Berg 01/08/2024 (<https://github.com/jyberg>) Version 1.5.1

## Introduction

Nextion Arduino library provides an easy-to-use way to manipulate Nextion serial displays.  
Old deprecated Enhanced Nextion Library with single display support can be found with Release tag 0.12.1

Nextion has also hidden commands see if intrested see link to UNUF project in Links section.

This new major updated library version has atleast following improvements:

- Added support for multiple nextion displays:  
  Note: Board need to support multiple simultaneus serial communication ports.
  - Recommendation initialize nextion instance using Nextion::GetInstance command Harware and Software interfaces supported
  - Nextion objects requires pointer to instance.
  - Instance callback functios must be initialized to instance object.
- Connection initialization improved.
- Serial communication stabilization improved.
- Implementation divided to ./src ans ./include folders
- `STD_SUPPORT` define replaced with platform ESP8266 define if other platforms supports needed std functionality add platform define with or (`||`).
- TFT file upload added to behing of NEX_ENABLE_TFT_UPLOAD define
- Documentation updated.
- Examples updated.
- platformIO development platformio.ini and .library.json added
- Version numbering uses now Semantic Versioning 1.0.0 (<https://semver.org/>)
  -Given a version number MAJOR.MINOR.PATCH, increment the:
    MAJOR version when you make incompatible API changes,
    MINOR version when you add functionality in a backwards compatible manner, and
    PATCH version when you make backwards compatible bug fixes.

Converting from old to new library version:

```c++
// Get Nextion display instance by defining:
// esp8266 / NodeMCU software serial ports
SoftwareSerial mySerial_D1(D2, D1); // RX, TX

// Declare Nextion instance
Nextion *next_D1 = Nextion::GetInstance(mySerial_D1); // uses software serial

// Declare a main page object and other objects
// Display instance is first parameter, and in page object component id is removed
NexPage p0_D1(next_D1, 0, "page0");

// Check nextion events using nextloop over Nextion instance
next_D1->nexLoop(nex_listen_list_D1);<br />
```

See `./examples` folder on how to use new version and multiple display support with esp8266/NodeMCU board!

Earlier improvements:

- Function return values corrected.
- systemStartUpCallback function pointer name corrected to match Nextion functionality/documentation new name: nextionReadyCallback.
- Error code list updated (`NexHardware.cpp`)
- nextionStartupCallback function added. Called when when Nextion has started or reset.
- Added support for NodeMcu/esp8266, Software serial, Software serial can be used with arduino.
- Added support for global Nextion objects. (Optional page parameter added in the components)
- NexVariable corrected to use int32_t data type.
- NextText corrected to return true/false, and string length is returned in len parameter.
- NextText String object support added.
- Other small bug fixes done.
- Added to support global Nextion events like `CurrentPageIdCallback`, `systemStartUpCallback`, ... see `NexHardware.h`
- Waveform corrections:
  - Inheritance to support toutch events.
  - set/get channel colour corrected to support all channels.
- Waveform enhancedments:
  - Suport scaled values:
  - define min and max values + coponent height in pixels (component support 255 pixel max height).  
  When value is added to change it is automatically scaled to component size and min/max value definitions.
  - Add multiple values to line.
  - Clear component.
- Added get component height/width function calls to `NexObject`.
- C style versions added for functions that uses `std::vector` etc..

## Suppported Mainboards

**All boards, which has one or more hardware serial, can be supported.**

For example:

- Iteaduino MEGA2560
- Iteaduino UNO
- Arduino MEGA2560
- Arduino UNO
- NodeMcu
- Esp8266

## Configuration

In configuration file `NexConfig.h`, you can configure:

- Define standard (default) or fast timeout, you may use fast timeout in case of baudrate higher than 115200
- Define `DEBUG_SERIAL_ENABLE` to enable debug serial, and used debug serial port
- Enable Next TFT file upload functionality
- Enable HardwareSerial support by defining `NEX_ENABLE_HW_SERIAL`
- Enable SoftwareSerial support by defining `NEX_ENABLE_SW_SERIAL`

If you want activate Debug messages, uncomment `//#define DEBUG_SERIAL_ENABLE` line and define serial port used for debug messges using line: `//#define dbSerial Serial`, it is responsibiity of main program to initialize/open debug serial port.  

## NodeMcu esp8266 connectivity tips

NodeMcu board pin numbers not match with Esp8266 pin numbers. So use `D<x>` pin number definitions from pins_arduino.h  
You need to remember that Software serial is not nessessary workin with out problmes at least when using NodeMcu/Esp8266 boards (See power tips...).

## Power tips

Nextion and NodeMcu/Esp8266 is sensitive with power quality and current. Especially when Software serial is used, (Serial message quality can be bad and then functionality is not stable...). Don't power Nextion display from NodeMcu/Esp8266 board, because Nextion takes guite mutch of current, and NodeMcu/Esp8266 internal power requlator is not good enough. Use separate power to power Nextion and connect Nextion and NodeMcu/Esp8266 board GND to commond GND point.  

## Useful Links

- <https://github.com/UNUF/nxt-doc/blob/main/Protocols/Full%20Instruction%20Set.md>
- <https://nextion.itead.cc/resources/download/nextion-editor/>
- <https://unofficialnextion.com/>
- <https://nextion.itead.cc/resources/download/nextion-editor/>
- <https://github.com/hagronnestad/nextion-font-editor>
- <http://blog.iteadstudio.com/nextion-tutorial-based-on-nextion-arduino-library/>
- <https://www.itead.cc/wiki/Nextion_Instruction_Set>
- <https://nextion.itead.cc/resources/documents/instruction-set/>
- <http://wiki.iteadstudio.com/Nextion_HMI_Solution>

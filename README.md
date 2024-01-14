# USB Relay

Simple 5V 2A Wi-Fi Relay with USB-C in and USB-A out. I'm using this to integrate decorative lights into a 
smart home environment, perhaps of interest for beginners as simple ESPHome and Fusion360 example project.

![case3.jpg](img%2Fcase3.jpg)

## BOM

* 1x USB-C female breakout
  https://de.aliexpress.com/item/1005005187670446.html
* 1x USB-A female breakout
  https://de.aliexpress.com/item/32983983188.html
* 1x AMS1117 3.3V regulator module
  https://de.aliexpress.com/item/1005005911922207.html
* 1x ESP-01S ESP8266 module
  https://de.aliexpress.com/item/1005006174109128.html
* 1x 2x4P female header socket
  https://www.aliexpress.com/item/1005001781173114.html
* 1x 5V DC relay
  https://de.aliexpress.com/item/1005004384333385.html
* 1x 3x7 double-sided prototyping PCB
  https://de.aliexpress.com/item/1005003384352824.html
* 1x 2N7000 N-channel MOSFET
  https://de.aliexpress.com/item/1005005945696455.html
* 1x 1N4148 diode
  https://de.aliexpress.com/item/1005006127068810.html
* 1x 100k resistor
* 1x 6x6x15 mini push button
  https://de.aliexpress.com/item/32912263133.html
* 4x 2x8 screw
  https://www.aliexpress.com/item/1005002322813833.html
* 4x 6x2mm rubber feet
  https://www.aliexpress.com/item/1005004068119765.html


## Schematic

![schematic.jpg](img%2Fschematic.jpg)


## PCB

![pcb3.jpg](img%2Fpcb3.jpg)
![pcb1.jpg](img%2Fpcb1.jpg)
![pcb2.jpg](img%2Fpcb2.jpg)
![pcb-wiring.jpg](img%2Fpcb-wiring.jpg)


## 3D printed case

![fusion.png](img%2Ffusion.png)
![case1.jpg](img%2Fcase1.jpg)
![case2.jpg](img%2Fcase2.jpg)


* Fusion 360 Archive: [usb-relay.f3d](cad%2Fusb-relay.f3d)
 
* [usb-relay-case.stl](cad%2Fusb-relay-case.stl)
* [usb-relay-lid.stl](cad%2Fusb-relay-lid.stl)
* [usb-relay-button.stl](cad%2Fusb-relay-button.stl)


## ESPHome

For initial programming, I used this adapter: https://de.aliexpress.com/item/1005003396937959.html

```yaml
esphome:
  name: usb-relay-02
  friendly_name: usb-relay-02

esp8266:
  board: esp01_1m

# Enable logging
logger:

# Enable Home Assistant API
api:

ota:
  password: "ef468b5d3eac4c58444d9c30628206c0"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Usb-Relay-02 Fallback Hotspot"
    password: "YR4r1ClyDioP"

captive_portal:

mqtt:
  broker: mqtt.lan

switch:
  - platform: gpio
    name: "relay"
    id: relay
    pin: 1
    inverted: True
    restore_mode: ALWAYS_OFF

binary_sensor:
  - platform: gpio
    name: button
    id: button
    pin:
      number: 2
      mode: INPUT_PULLUP
      inverted: True
    on_press:
      then:
        - switch.toggle: relay

```

## License

This is free and unencumbered software and data released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <https://unlicense.org>

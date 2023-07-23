# Project Supernova
A Helium Balloon, to assess the Helium Network.

## Features
This project is a PCB which is capable of being the primary payload on a PCB aboard a stratospheric helium balloon. The PCB intends to downlink 

* Onboard GPS for position tracking
* Atmospheric condition sensors (temperature/pressure/humidity) to generate downlink data
* Onboard PID-controlled heater and battery management
* Very low cost (<$100)

## Notes
* 3v3 regulated voltage. 9v unregulated battery voltage.
 
## Rev 2 Errata
1. Nothing yet (fingers crossed)

## Rev 1 Errata
1. DHT22 doesn't support 3V3 supply, technically
2. ADC2 doesn't work when wifi is enabled
3. DHT22 cannot be connected to pin D12, as D12 must be floating at boot
4. D34-D39 are input-only (so `TEMP_V+` is a problem)
5. LM335 onboard temperature sensor is basically incompatible with 3V3 systems
6. DHT22 needs a 10k pull-up to 3V3
7. RTF switch needs resistors on each leg to prevent shorting in case of a make-before-break switch.
8. The voltage regulator footprint could use the pads moved a bit (and could include through-hole pins).
9. Should've added a pull-down resistor to the heater MOSFET to prevent heating during boot.
10. Shouldn't have put a via in the pad on the MOSFET, as it prevented the gate from soldering right, then burned the MOSFET when it entered the linear region. Should've used way larger pads on the hand-soldered SOT-23 MOSFET.

### Changes made to correct errata items (Rev 1.1)
* DHT22 (`DHT_DATA`) now connected to D23 (per Errata #3).
* DHT22 now has a 10k pull-up to 3V3 (Errata #6).
* `TEMP_V+` now connected to D25 (per Errata #4), and still left connected to D35.
* LM335 onboard temperature sensor is unused.

### OFIs
* Add LED on HEATER_EN net
* Add LED polarity on silk screen
* Consider 10u cap from GND to EN for programming
* D2 is the onboard LED, so probably best to not use it
* Should have referenced this doc: https://randomnerdtutorials.com/esp32-pinout-reference-gpios/
* Add jumper to disconnect power from GPS (because it uses so much power)

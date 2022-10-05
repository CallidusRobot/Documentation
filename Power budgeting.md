# Power budgeting

## LiPo
2S LiPo ~7.4V

### Current sinks
* ~2,7A buck to 5V
* TBD A for motors

## First level regulation to 5V
S13V30F5 Boost-Buck 2.8-22V input voltage, 4A sustained output current

### Output current capability
![image](https://user-images.githubusercontent.com/2276327/194172997-f22ad231-0863-4519-8dbf-07bdbd8925af.png)

### Current sinks
* 2A for LEDs (DMD, WS2812)
* 1A for Sound-Player
* 1A for Control (Pico, WiFi, sensors)

## Second level regulation to 3.3V
### Raspberry Pi Pico @ 300mA
* Pico itself
* WiFi Module (up to 300mA, move to linear reg?)

### LDI1117-3.3U-DIO @ 1.35A
* RFID
* Magnetometer
* VL53L3X
* Line tracker
* Motor-Driver (just logic)

# Hardware
- RFID (SPI0)
- RGB-DMD (I2C0 level shifted)
- WS2812 (GPIO level shifted)
- Magnetometer (I2C0)
- WiFi (UART0)
- Sound-Player (UART1)
- Multi-target sensor VL53L3X (I2C0)
- Motor driver TB66FNG (GPIO + PWM)
- Line tracker (ADC + GPIO)
- Personality I2C EEPROM 24FC01T (I2C0)
- Battery supply: 5V and 3V3 regulators, Motor-Driver (motor power)
- 5V power supply @ 2.5A: Raspberry Pi Pico, RGB-DMD, WS2812, Sound-Player
- 3V3 pico supply @ 300mA: RFID, Magnetometer, VL53L3X, Line tracker, Motor-Driver (just logic)
- 3V3 power supply @ 500mA: WiFi

## TODO
- Add accelerometer to block diagram and schematics via QWIIC to magnetometer
- Design schematics
- Design PCB
- Order PCB
- Buy level-shifters, capacitors, connectors and 3V3 regulators

## Block diagram
![Block diagram](Block%20diagram.png)

## Pin allocation
- SPI0: 3 (MOSI0, MISO0, SCK0) + 1 (RFID_SS) + opt. 2 (RFID_RESET, RFID_IRQ)
- I2C0: 2 (SDA0, SCL0) + 1 (VCSEL_XSHUT)
- UART0: 2 (RX0, TX0)
- UART1: 2 (RX1, TX1) + 1 (PLAYER_BUSY)
- WS2812: 2 (GPIO level shifted)
- Motor driver: 2 (PWM) + 5 (GPIO)
- Line tracker: 2 (ADC + GPIO)
- Heartbeat LED: 1 (Pin 25 internal)
- WiFi Power down (via open-drain inverter)

Total used/available: 27/27 (all used)

## RFID
SPI

https://www.berrybase.de/rfid-lesegeraet-mit-spi-schnittstelle-inkl.-karte-dongle

- MOSI
- MISO
- SCK
- SS
- RESET
- IRQ
- 3V3

## RGB-DMD
13x9 RGB565, I2C

https://www.berrybase.de/adafruit-is31fl3741-13x9-pwm-rgb-led-matrix-treiber

- SDA
- SCL
- Power at 5V (looks better) and use I2C level shifter (could be powered at 3V3, but high power consumption is bad)

## WS2812
WS2812 (level shifted to 5V), 63cm ~ 38 LEDs, 60 LED/m, 60mAp/LED, Protection series resistor 330R, 100-1000uF decoupling

- OUT
- 5V

## Magnetometer
I2C

https://www.berrybase.de/adafruit-drei-achsen-magnetometer-lis3mdl

- SDA
- SCL
- 3V3

## WiFi
UART, Firmware update passthrough

- RX
- TX
- 3V3

## Personality I2C EEPROM 24FC01T
I2C

https://www.tme.eu/de/details/24fc01t-i_ot/serielle-eeprom-speicher/microchip-technology/

- SDA
- SCL
- 3V3

## Sound Player
UART @ 9600 8N1

https://www.berrybase.de/mp3-player-modul-mit-eingebautem-verstaerker

- RX
- TX
- 3V3

## Multi-target sensor VL53L3X
I2C

https://www.berrybase.de/pololu-vl53l3cx-time-of-flight-multi-target-distanzsensor-mit-spannungsregler-bis-500cm

- SDA
- SCL
- XSHUT
- 3V3

## Motor driver TB66FNG
PWM GPIO

https://www.berrybase.de/sparkfun-motor-treiber-dual-tb6612fng-mit-headern

- PWMA (SPEED1)
- PWMB (SPEED2)
- AIN1 (DIR1)
- AIN2 (DIR1)
- BIN1 (DIR2)
- BIN2 (DIR2)
- STBY
- 3V3
- 8V

## Line tracker
ADC GPIO

https://www.pololu.com/product/4641

- Analog signal pin
- Enable pin

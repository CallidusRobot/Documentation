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
- Battery voltage supervision ADC (I2C0)
- Battery supply: 5V and 3V3 regulators, Motor-Driver (motor power)
- 5V power supply @ 2.5A: Raspberry Pi Pico, RGB-DMD, WS2812, Sound-Player
- 3V3 pico supply @ 300mA: Motor-Driver (just logic), EEPROM, other logic ICs
- 3V3 power supply @ 500mA: WiFi, RFID, Magnetometer, VL53L3X, Line tracker

## TODO
- (Add accelerometer to block diagram and schematics via QWIIC to magnetometer)
- Add EEPROM, VBAT ADC and 3V3 regulator supervision (status, off) to block diagram
- Design schematics
- Design PCB
- Order TME parts
- Order PCB

## Block diagram
![Block diagram](Block%20diagram.png)

## Pin allocation
- SPI0: 3 (MOSI0, MISO0, SCK0) + 1 (RFID_SS) + opt. 2 (RFID_RESET, RFID_IRQ)
- I2C0: 2 (SDA0, SCL0)
- UART0: 2 (RX0, TX0)
- UART1: 2 (RX1, TX1) + 1 (PLAYER_BUSY)
- WS2812: 2 (GPIO level shifted)
- Motor driver: 2 (PWM) + 5 (GPIO)
- Line tracker: 2 (ADC + GPIO)
- Heartbeat LED: 1 (Pin 25 internal)
- External 3V3 power down, regulator status

Total used/available: 27/27 (all used)

## RFID
SPI

https://www.berrybase.de/rfid-lesegeraet-mit-spi-schnittstelle-inkl.-karte-dongle

- MOSI
- MISO
- SCK
- SS
- RESET (Probably not needed; could be used to replace I2C ADC)
- IRQ
- 3V3

## RGB-DMD
13x9 RGB565, I2C

https://www.berrybase.de/adafruit-is31fl3741-13x9-pwm-rgb-led-matrix-treiber

- SDA
- SCL
- Power at 5V (looks better) and use I2C level shifter (could be powered at 3V3, but looks better at 5V)

## WS2812
WS2812 (level shifted to 5V), 60 LED/m, 60mAp/LED, Protection series resistor 330R, 100-1000uF decoupling

Shield: 63cm -> 37 LEDs, 2.22Ap, 3mm spaced from top of shield

Cannon: TBD

- OUT
- 5V

## Magnetometer
I2C

https://www.berrybase.de/adafruit-drei-achsen-magnetometer-lis3mdl

- SDA
- SCL
- 3V3E

## WiFi
UART, Firmware update passthrough

- RX
- TX
- 3V3E

## Personality I2C EEPROM 24FC01T
I2C

https://www.tme.eu/de/details/24fc01t-i_ot/serielle-eeprom-speicher/microchip-technology/

- SDA
- SCL
- 3V3I

## Battery voltage supervision ADC
I2C

Could be replaced with spare pin on Pico if e.g. NFC_RESET is dropped

https://www.tme.eu/de/details/mcp3221a0t-e_ot/a-d-wandler-integrierte-schaltungen/microchip-technology/

- SDA
- SCL
- 3V3A (via ADC-VREF on Pico)

## Sound Player
UART @ 9600 8N1

https://www.berrybase.de/mp3-player-modul-mit-eingebautem-verstaerker

- RX
- TX
- 5V

## Multi-target sensor VL53L3X
I2C

https://www.berrybase.de/pololu-vl53l3cx-time-of-flight-multi-target-distanzsensor-mit-spannungsregler-bis-500cm

- SDA
- SCL
- 3V3E

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
- 3V3I
- 8V

## Line tracker
ADC GPIO

https://www.pololu.com/product/4641

- Analog signal pin
- Enable pin
- 3V3E

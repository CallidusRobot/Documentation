# Hardware
- RFID (SPI0)
- RGB-DMD (I2C0)
- WS2812 (17-5V)
- Magnetometer (I2C0)
- WiFi (UART0)
- Sound-Player (UART1)
- Multi-target sensor VL53L3X (I2C0)
- Motor driver TB66FNG (GPIO + PWM)
- Battery supply: 5V and 3V3 regulators, Motor-Driver (motor power)
- 5V power supply @ 2.5A: Teensy, RGB-DMD, WS2812
- 3V3 power supply @ TBDmA: RFID, Magnetometer, WiFi, Sound-Player, VL53L3X, Motor-Driver (just logic)

# Pin allocation
- SPI0: 3 (MOSI0, MISO0, SCK0) + 1 (RFID_SS) + opt. 2 (RFID_RESET, RFID_IRQ)
- I2C0: 2 (SDA0, SCL0)
- UART0: 2 (RX0, TX0)
- UART1: 2 (RX1, TX1) + 1 (PLAYER_BUSY)
- WS2812: 1 (17/17-5V)
- Motor driver: 2 (PWM) + 5 (GPIO)
- Heartbeat LED: 1 (opt.)
- Firmware update sw: 1 (opt.)

Total used/available: 23/23 (all used)

## TODO
- Check for I2C collisions
- Check how much current is needed on 3V3
- Design schematics
- Buy level-shifters, capacitors, connectors, 5V and 3V3 regulators
- Design PCB
- Order PCB

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
WS2812 (17-5V), 60mAp/LED, Protection series resistor 330R, 100-1000uF decoupling

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

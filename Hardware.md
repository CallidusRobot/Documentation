# Hardware
- RFID (SPI0)
- RGB-DMD (I2C0 level shifted)
- WS2812 (GPIO level shifted)
- Magnetometer (I2C0)
- WiFi with power control (UART1 + GPIO)
- Sound-Player (UART0)
- Multi-target sensor VL53L3X (I2C0)
- Motor driver TB66FNG (GPIO + PWM)
- Line tracker (ADC + GPIO)
- Personality I2C EEPROM 24FC01T (I2C0)
- Battery voltage measurement (ADC2)
- Battery supply: 5V and 3V3 regulators, Motor-Driver (motor power)
- 5V power supply @ 2.5A: Raspberry Pi Pico, RGB-DMD, WS2812, Sound-Player, WiFi
- 3V3 pico supply @ 300mA: Motor-Driver (just logic), RFID, Magnetometer, VL53L3X, Line tracker, EEPROM, other logic ICs

## TODO
- Add accelerometer to diagram and this document
- Check, if RFID is really compatible, else buy RFID cards
- Print replacement arrow label for WiFi header on PCB
- Assemble PCBs
- Make custom cables

## Block diagram
![Block diagram](Block%20diagram.png)

## Pin allocation
- SPI0: 3 (MOSI0, MISO0, SCK0) + 2 (RFID_SS, RFID_IRQ)
- I2C0: 2 (SDA0, SCL0)
- UART0: 2 (RX0, TX0) + 2 (WIFI_ENABLE, WIFI_FAULT)
- UART1: 2 (RX1, TX1) + 1 (PLAYER_BUSY)
- WS2812: 2 (GPIO level shifted)
- Motor driver: 2 (PWM) + 5 (GPIO)
- Line tracker: 2 (ADC + GPIO)
- Battery supervision: 1 (ADC)
- Heartbeat LED: 1 (Pin 25 internal)

Total used/available: 27/27 (all used)

## Pico Pinout
- GP0: OUT: MOTOR_PWMB
- GP1: OUT: MOTOR_BI2
- GP2: OUT: MOTOR_BI1
- GP3: OUT: MOTOR_STBY, active-low
- GP4: OUT: MOTOR_AI1
- GP5: OUT: MOTOR_AI2
- GP6: OUT: MOTOR_PWMA
- GP7: INP: RFID_IRQ, probably unused, int-pullup or int-pulldown as configured, could be reset output instead
- GP8: OUT: WIFI_TX
- GP9: INP: WIFI_RX
- GP10: OUT: RFID_CK
- GP11: INP: RFID_TX
- GP12: OUT: RFID_RX, int-pulldown
- GP13: OUT: RFID_CD
- GP14: INP: WIFI_FAULT, active-low, int-pullup
- GP15: OUT: WIFI_ENABLE, active-high
- GP16: OUT: SOUND_TX
- GP17: INP: SOUND_RX, int-pullup
- GP18: OUT: WS2812_A
- GP19: OUT: WS2812_B
- GP20: BID: I2C0_SDA
- GP21: OUT: I2C0_SCL
- GP22: INP: SOUND_BUSY, int-pullup, high = idle, low = playing
- GP23: OUT: 3V3 SMPS power save mode
- GP24: INP: VBUS sense (is USB plugged in)
- GP25: OUT: Heartbeat LED
- GP26: ADC: LINE_REFLECTANCE
- GP27: OUT: LINE_ENABLE
- GP28: ADC: VBAT minus drop over U3, then divided
- GP29: ADC: VSYS/3 = 5V SMPS / 3

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

- OUT1
- OUT2
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
- ENABLE
- FAULT
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
- 5V

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

## Line tracker
ADC GPIO

https://www.pololu.com/product/4641

- Analog signal pin
- Control pin
- 3V3

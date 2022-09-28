# Hardware
- RFID (SPI0)
- RGB-DMD (I2C0)
- Magnetometer (I2C0)
- WiFi (UART0)
- Sound-Player (UART1)

## RFID
SPI

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
- Power at 5V (looks better) and use I2C level shifter or power at 3V3

## Magnetometer
I2C

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

- RX
- TX
- 3V3



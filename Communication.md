# Communication

Timeout for each packet of 100ms. Reset with packet drop after timeout.

## Packets
- 0x55
- Packet-ID (1B)
- Type (1B)
- Length (1B)
- Payload (nB)
- CRC-16 (2B)

## Types
- High-Bit 0: Command
- High-Bit 1: Status

### Commands
Zero is reset

### Statuses
Zero is success, everything else is failure


## Internal movement correction
- Calibrate against accelerometer and compass
- Use NFC to home

## Movement format
- Polar coordinates: absolute compass direction (16 bit unsigned full-scale) plus distance from home

## Configuration messages

## Ping message
- Source of the ping
  - WIFI/Camera
  - Server
  - Controller
- Value to return

## Trigger message
There must be a way to trigger the scheduled DMD/Shield/Cannon/Motor updates quickly and on all robots at the same time

- Delay in ms after which to trigger (can be zero)
- Bitfield of what updates to perform after delay
  - Motor
  - DMD
  - Shield
  - Cannon

## Request message
Requests the transmission of a message

- What to request
  - System
  - Power
  - WiFi status
  - Sensors
  - Sound status

## Reset message
Resets the scheduled data for the particular peripheral. Also treats transparency as black for the next respective update.

- Bitfield of what to reset
  - Motor
  - DMD
  - Shield
  - Cannon

## System message
- Version info
- Contents of the personality EEPROM

## WiFi status message
- Network name prefixed by string length (if already set)
- RSSI (signal strength or zero if disconnected)

## WiFi AP message
- Connect/disconnect
- Network name
- Password

## Write personality message
- New contents of the personality EEPROM

## Power message
- Bitfield
  - State of the WiFi power failure flag
  - Whether USB is connected
  - Whether the battery is operational
- Battery voltage
- System voltage (5V)

## Sensor message
- Accelerometer data
- Gyroscope data
- Magnetometer data
- Line sensor data

## DMD message
- Number of palette entries (usable entries start at one, zero is transparent)
  - Palette entries in RGB565
- Frame duration in ms (negative = no loop, positive = loop)
- Number of frames
  - Origin x of the area to update
  - Origin y of the area to update
  - Width of the area to update
  - Height of the area to update
  - Palettized frame data with one byte per pixel

## Shield message
- Number of palette entries (usable entries start at one, zero is transparent)
  - Palette entries
    - Hue
    - Saturation
- Frame duration in ms
- Number of frames
  - Start position of the first LED to update
  - Number of LEDs to update
  - Palettized frame data with two bytes per LED
    - Palette index
    - Brightness value

## Cannon message
The same as the shield message.

## Sound message
- Message type (play effect/music, pause effect/music, stop effect/music, volume)
- Background music number/volume

## Sound status message
- Status bitfield
  - Card and module ready
  - Currently playing
- Currently playing background music (or none)
- Currently playing sound effect (or none)
- Volume

## RFID message
- Depending on RFID configuration returns a number of sectors starting at zero
- Only cards with a SAK of 08 (MIFARE 1K) are supported

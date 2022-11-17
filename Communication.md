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

## DMD message
- Number of palette entries (usable entries start at one, zero is transparent)
  - Palette entries in RGB565
- Frame duration in ms (negative = no loop, positive = loop)
- Number of frames
  - Origin x of the area to update
  - Origin y of the area to update
  - Width of the area to update
  - Height of the area to update 
  - Frame data with one byte per pixel

## RFID message
- Depending on RFID configuration returns a number of sectors starting at zero
- Only cards with a SAK of 08 (MIFARE 1K) are supported

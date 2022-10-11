# Intra-Robot Kommunikation

Paket darf höchstens 100ms übertragen werden. Danach Reset und neues Paket.

## Pakete
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

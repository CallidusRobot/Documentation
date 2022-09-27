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
High-Bit: Command/Status

### Commands
Zero is reset

### Statuses
Zero is success, everything else is failure

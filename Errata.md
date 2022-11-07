# Errata

## PCB
- WiFi RX and TX are correctly wired but the arrows are swapped (ordered V12, fixed in V13)
- RFID RX and TX are correctly wired but the arrows are swapped (fixed in V14)
- Battery monitoring (VBAT) voltage-divider is incorrectly wired (see fix, fixed in V15)

## Battery monitoring fix
![grafik](https://user-images.githubusercontent.com/2276327/200320227-e426e829-cfee-409f-a398-1cd14c8d96ec.png)

- Populate R16 with a 0 Ohm jumper
- Solder a 2.2k resistor between R16 (right) and C8 (left)
- This forms the lower part of the voltage divider to ground

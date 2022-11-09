# Errata

## PCB
- WiFi RX and TX are correctly wired but the arrows are swapped (ordered V12, fixed in V13)
- RFID RX and TX are correctly wired but the arrows are swapped (fixed in V14)
- Battery monitoring (VBAT) voltage-divider is incorrectly wired (see fix, fixed in V15)
- Maximum input voltage is 18V, not 20V as printed on the PCB (fixed in V15)
- U2 VCC has no connection to 3V3 (see fix)
- U3 has no IOFF and therefore feeds back 3V7 into 3V3 when there is no 3V3 regulator

## Battery monitoring fix
![grafik](https://user-images.githubusercontent.com/2276327/200320227-e426e829-cfee-409f-a398-1cd14c8d96ec.png)

- Populate R16 with a 0 Ohm jumper
- Solder a 2.2k resistor between R16 (right) and C8 (left)
- This forms the lower part of the voltage divider to ground

## U2 VCC fix
![grafik](https://user-images.githubusercontent.com/2276327/200917748-4fef5717-1962-4cd3-a04b-cf5b16bd0990.png)

Add a connection between C3 (right) and R7 (right)

# Power budgeting

## LiPo
2S LiPo ~7.4V

## First level regulation to 5V
S13V30F5 Boost-Buck 2.8-22V input voltage, 4A sustained output current

![image](https://user-images.githubusercontent.com/2276327/194172997-f22ad231-0863-4519-8dbf-07bdbd8925af.png)

## Second level regulation to 3.3V
* Raspberry Pi Pico @ 300mA
* LDI1117-3.3U-DIO @ 1.35A
* Inside various components itself, including Sound-Player

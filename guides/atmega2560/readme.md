# Initial Programming ATmega2560

## Prerequisites
* an AVR ISP programmer, such as the official  [ATMEL-ICE programmer](https://www.microchip.com/en-us/development-tool/atatmel-ice) or a standard [Arduino device](https://www.arduino.cc/en/Main/Products) with ISCP interface like an *Arduino UNO*
* if programmer is an Arduino device, then 6 male/female pin jumper cables
* local PC with USB interface

The ATmega2560 is the brains of the Farmduino PCB. It talks with the Raspberry Pi using the ATmega16U2 as bridge. In this tutorial the USB host will be your local PC first instead of the Raspberry PI 3B+.

|Actors |Connection|Properties|
|-|-|-|
|Host PC <--> atmega16U2|USB 2.0|Serial; Full-Speed max. 12Mbit/s; Half-Duplex; ; one differential line pair ```d+``` and ```d-```|
|atmega16U2 <--> atmega260|UART|Serial;  115.200 baud; Full-Duplex; one ```TX``` transmitting line, one ```RX``` receiving line

## Programming

Fresh from factory an ATmega2560 won't have the bootloader loaded onto the SoC. To flash the bootloader, you will need an ISP programmer such as the official [ATMEL-ICE programmer](https://www.microchip.com/en-us/development-tool/atatmel-ice). But an official Arduino standard device will do, too. I used an Arduino UNO.

### Physical Setup

The atmega2560 circuit of the Farmduino PCB comes with an ISCP interface to program the SoC. It is 2x3 pin header located at the lower right side of the PCB.

![atmega2560](/guides/atmega2560/iscp-atmega2560.png) 

You will need to connect those 6 pins on the Farmduino PCB with jumper cables to their counterparts on the programmer, in my case an Arduino Uno. Make sure none of the devices is powered during wiring!

|Farmduino ISCP|Arduino Uno|
|-|-|
|`MOSI`|`Digital pin 11`|
|`MISO`|`Digital pin 12`|
|`SCK`|`Digital pin 13`|
|`USBVCC`|`POWER 5V`|
|`RESET`|`Digital pin 10`|
|`USBGND`|`GND`|

Once you are finished, it should look similar like this.
![atmega2560](/guides/atmega2560/wiring.png)

### Software setup

I used the official [Arduino IDE](https://www.arduino.cc/en/software), because it comes with the right firmware for the ATmega2560 already and is able to program the Farmduino PCB trough an Arduino device. You can *avrdude* commandline tool for the same task too.

To configure an Arduino device as programmer, you will need to upload a program called `ArduinoISP`.

1. Connect your local PC with the Arduino via USB once all the ISCP cabling is done
2. Open [Arduino IDE](https://www.arduino.cc/en/software).
3. Load the sketch by opening `File menu` -> `Examples`-> `11.ArduinoISP`-> `ArduinoISP`
4. Open `tools menu` and select `Arduino Uno` as Board
5. Open `tools menu` and select `ATmega2560 (Mega2560)` as Processor
6. Open `tools menu` and select the right `COM port [n]` as Port
7. Open `tools menu` and select `AVRISP mkll` as Programmer
8. Open `sketch menu` and select `Upload`

### Burning the bootloader

Use Arduino IDE again.

1. Open `tools menu` and select `Arduino Mega or Mega 2560` as Board
2. Open `tools menu` and select `ATmega2560 (Mega2560)` as Processor
3. Open `tools menu` and select the right `COM port [n]` as Port
4. Open `tools menu` and select `Arduino as ISP` as Programmer
5. Open `tools menu` and select `Burn Bootloader`

If all goes well, Arduino IDE will confirm the flashing of the bootloader. During burn procedure some LEDs on the Farmduino Board will flash wildly. After this sequence the default application has been loaded which causes the `GRE1` LED to flash two times in a row ... forever.

Done.
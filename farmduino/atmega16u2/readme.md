# Initial Programming of ATmega16U2

## Prerequisites
* an AVR ISP programmer, such as the official  [ATMEL-ICE programmer](https://www.microchip.com/en-us/development-tool/atatmel-ice) or a standard [Arduino device](https://www.arduino.cc/en/Main/Products) with ISCP interface like an *Arduino UNO*
* if programmer is an Arduino device, then 6 male/female pin jumper cables
* local PC with USB interface

The ATmega16U2 serves as serializer between USB host and ATmega2560. The USB host may be your local PC at this time and later the Raspberry PI 3B+ with FarmOS running on it. 

|Actors |Connection|Properties|
|-|-|-|
|Host PC <--> atmega16U2|USB 2.0|Serial; Full-Speed max. 12Mbit/s; Half-Duplex; ; one differential line pair ```d+``` and ```d-```|
|atmega16U2 <--> atmega260|UART|Serial;  115.200 baud; Full-Duplex; one ```TX``` transmitting line, one ```RX``` receiving line

The SoC comes with the factory default firmware which won't act as serializer. You will need to update the firmware as described below, otherwise you won't be able to program ATmega2560 through USB.

## Electrical test
The USB-B port needs to be powered by connecting it to the local PC using an USB/B-to-USB/A cable. The USB circuit on the PCB is decoupled from all other circuits. Your PC will be USB host and the board the USB device. Power goes downstream from USB host to device.

Check wether or not the ATmega16U2 SoC is powered with the help of an oscilloscope. I use the Rigol DS1043Z. Connect the probe to the *VCC*, *AVCC* and *UVCC* pins, because all of them are powered through the USB-B power lines. The voltage level should be about 5V at each pin. If not, there is an issue with USB power supply.

![atmega16u2](/guides/atmega16u2/atmega16u2.png)

## Install Windows atmega16U2 driver
Use [Atmel Flip](https://www.microchip.com/en-us/development-tool/flip) software to connect to the ATmega16U2. I used Windows 11. Please note Flip requires a 32-bit Java JRE to start properly. Make sure Java binaries are added to PATH environment variables. 

If necessary install the Atmel USB driver *AtLibUsbDfu.dll* manually. It is located in *USB* directory of the Flip installation directory. Open Windows device manager and look for "unknown device". Right click the entry and select "update driver". Then select "search for driver on computer" and navigate to 

```bash
Your\Path\..\Atmel\Flip 3.4.7\usb
```

or where you installed Flip. Confirm the directory. The computer will find the correct driver and installs it. Plug the USB-A end of USB cable into your PC and connect it to the USB-B port of your Farmduino. In the device manager the SoC should show up as follows:

![atmega16u2](/guides/atmega16u2/device-manager.png)

## Programming

To enable the external crystal oscillator the fuses bits have to be changed. You will need an ISP programmer such as the official [ATMEL-ICE programmer](https://www.microchip.com/en-us/development-tool/atatmel-ice). But an official Arduino standard device will do, too. I used an Arduino UNO.

### Physical Setup

The USB circuit of the Farmduino PCB comes with an ISCP interface to program the ATmega16U2.

![atmega16u2](/guides/atmega16u2/iscp-atmega16U2.png) 

You will need to connect those 6 pins on the Farmduino PCB with jumper cables to their counterparts on the programmer, in this case an Arduino Uno. Make sure none of the devices is powered during wiring!

|Farmduino ISCP|Arduino Uno|
|-|-|
|`MOSI`|`Digital pin 11`|
|`MISO`|`Digital pin 12`|
|`SCK`|`Digital pin 13`|
|`USBVCC`|`POWER 5V`|
|`RESET`|`Digital pin 10`|
|`USBGND`|`GND`|

Once you are finished, it should look similar like this.
![atmega16u2](/guides/atmega16u2/wiring.png) 

Now it is time to connect the Arduino to your local PC through USB. The atmega16u2 will programmed with the Arduino as programmer. 

### Retrieval of meta data

Use *avrdude* program to get a detailled list of current ATmega16U2 parameters. *Avrdude* ships with the official [Arduino IDE](https://www.arduino.cc/en/software). Make sure you replace the path and COM port with your actual settings. It is important to work with `19200` as baud rate during programming.

```bash
avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -b 19200
```

Commandline parameters explained.
|Parameter|What it does|
|-|-|
|`-p m16u2`|the Atmel SoC that is addressed with the call, in this case ATmega16U2|
|`-c wiring`|protocol used for talking to Atmel SoC; wiring corresponds to STK500v2 internally which in turn is successor of STK500v1 and considered more stable|
|`-P COM3`|local communication port; here in Windows notation COM[n]|
|`-C avrdude.conf`|local path to avrdude configuration file|
|`-vvv` | verbose log of the communication with the SoC|
|`-c avrisp`|local PC is used as programmer|
|`-b 19200`|if programming is done through an Arduino device, then baud rate must be set `19200` to work properly|

If all goes well you will be presented an exhaustive list of your ATmega16U2 settings.

## Unlock the SoC

If ATmega16U2 comes fresh from the factory, then is has protection bits set and is locked. To unlock do the following steps. Otherwise you might not be able to change the fuses values.

1. Execute avrdude in the commandline.
```bash
avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -b 19200 -F -t
```
2. You will see this prompt `avrdude>`. Enter the phrase `erase`. Enter.
3. Write `quit` into console and then enter.

New commandline parameters explained.
|Parameter|What it does|
|-|-|
|`-F`|The device signatures will most likely not match, so the `-F` command tells avrdude to ignore them|
|`-t`| allows to enter the erase command|

### Configure the external crystal oscillator by setting fuses

By default the atmega16U2 uses an internal clock. The farmduino comes with a 16Mhz external crystal oscillator. ATmega16U2 needs to be configured to use the crystal by writing the fuses in order to synchronize with atmega2560, also running 16Mhz. On the PCB the crystal is located at the lower left side of the atmega16U2 marked with designator *G2*. The crystal is the clock generator for the atmega16U2 for synchronizing events within the SoC.

![atmega16u2](/guides/atmega16u2/crystal.png)

The standard settings of the fuses need to change in order to get the circuit up and running. There is a nice online tool called [*AVR Fuse Calulator*](https://www.microchip.com/en-us/development-tool/flip) for showing all options with corresponding bit masks. Two things have to be adressed here:
1. configure external 16Mhz crystal oscillator; 
  
    *`Ext. Crystal Osc.;Frequency 8.0-Mhz; Start-up time: 16K CK + 65ms; [CKSEL=1111 SUT=11]`*

2. remove flag that divides clock by 8

The final fuse values according to the previous configuration are:
|LOW|HIGH|EXTENDED|
|-|-|-|
|`0xFF`|`0xD9`|`0xF4`|

The values are programmed with *avrdude* tool. 

```bash
avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -b 19200 -U lfuse:w:0xff:m -U hfuse:w:0xd9:m -U efuse:w:0xf4:m
```

Additional parameters explained.
|Parameter|What it does|
|-|-|
|`-U`|says you like to deal with the fuses|
|`lfuse:w:0xff:m`|write LOW fuse with value `0xFF`|
|`hfuse:w:0xff:m`|write HIGH fuse with value `0xD9`|
|`efuse:w:0xff:m`|write EXTENDED fuse with value `0xF4`|

If all goes well *avrdude* will show a summary of the new fuse values.

## Flash usbserial application

You can use the *avrdude* again to flash the usbserial firmware onto the device. The right `hex` firmware is located in the *avrdude* installation directory.

```bash
C:\Program Files\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\arduino-usbserial\Arduino-usbserial-atmega16u2-Mega2560-Rev3.hex
```

Use *avrdude* in the commandline to flash the usbserial program onto the ATmega16U2 using the following command. Don't miss the `:i` at the end of the command if you are on Windows.

```bash
avrdude.exe -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -c arduino -P COM3 -b 19200 -p m16u2 -vvv -U flash:w:"C:\Program Files\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\arduino-usbserial\Arduino-usbserial-atmega16u2-Mega2560-Rev3.hex":i
```
Done.
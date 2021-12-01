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

![atmega16u2]/guides/atmega16u2/(/atmega16u2.png)

## Install Windows atmega16U2 driver
Use [Atmel Flip](https://www.microchip.com/en-us/development-tool/flip) software to connect to the ATmega16U2. I used Windows 11. Please note Flip requires a 32-bit Java JRE to start properly. Make sure Java binaries are added to PATH environment variables. 

If necessary install the Atmel USB driver *AtLibUsbDfu.dll* manually. It is located in *USB* directory of the Flip installation directory. Open Windows device manager and look for "unknown device". Right click the entry and select "update driver". Then select "search for driver on computer" and navigate to 

```bash
Your\Path\..\Atmel\Flip 3.4.7\usb
```

or where you installed Flip. Confirm the directory. The computer will find the correct driver and installs it. Plug the USB-A end of USB cable into your PC and connect it to the USB-B port of your Farmduino. In the device manager the SoC should show up as follows:

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2/device-manager.png" width="500">
</a>

## Flash usbserial application

Make sure your Farmduino is connected via USB cable to the local PC. Open a connection to atmega16U2 using Flip.

1. Open Flip
2. Select the microcontroller. 
3. Click “Device”>”Select…”, or use the shortcut key <Ctrl>+S
4. Select the microcontroller “ATMEGA16U2”.
5. Select the communication. 
6. Click “Settings”>”Communication”>”USB”, or use the shortcut key <Ctrl>+U.
7. A dialogue box may appear. Then click open. 

Flip will output some additional SoC data, such as hardware ID (signature bytes) and others. Do the *blank check* to verify the SoC is up and running.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2/flip.png" width="500">
</a>

Please note, an ATmega16U2 fresh from the factory has lock protection bits set. That means Flip won't be able to read the memory. But it could write an application as `HEX` file or a flash a new bootloader other than the default ATMEL DFU bootloader. We need the usbserial application located in the Arduino installation directory

```bash
C:\Program Files\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\Arduino-usbserial-atmega16u2-Mega2560-Rev3.hex
```
Load the usbserial firmware with FLIP. 

1. Click “File”>”Load HEX File…”>”Arduino-usbserial-atmega16u2-Uno-Rev3.hex”
2. Ensure the check box is checked. “Erase”, “Program” and “Verify”
3. Click “Run”.

Once the firmware is loaded, you can unplug the USB connection. The atmega16U2 won't be visible anymore.

## Configuration of fuses

To enable the external crystal oscillator the fuses bits have to be changed. You will need an ISP programmer such as the official [ATMEL-ICE programmer](https://www.microchip.com/en-us/development-tool/atatmel-ice). But an official Arduino standard device will do, too. I used an Arduino UNO.

### Physical Setup

The USB circuit of the Farmduino PCB comes with an ISCP interface to program the atmega16U2.

Use *avrdude* program to get a detailled list of current ATmega16U2 parameters. *Avrdude* ships with the official [Arduino IDE](https://www.arduino.cc/en/software). 

```bash
avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -b 115200
```

Commandline parameters explained
|Parameter|What it does|
|-|-|
|`-p m16u2`|the Atmel SoC that is addressed with the call, in this case ATmega16U2|
|`-c wiring`|protocol used for talking to Atmel SoC; wiring corresponds to STK500v2 internally which in turn is successor of STK500v1 and considered more stable|
|`-P COM3`|local communication port; here in Windows notation COM[n]|
|`-C avrdude.conf`|local path to avrdude configuration file|
|`-vvv` | verbose log of the communication with the SoC|
|`-c avrisp`|local PC is used as programmer|
|`-b 115200`|if local PC is programmer then 115200 is default; if programming is done through an Arduino instead (--> troubleshooting section), then it must be 19200 to work properly|

By default the atmega16U2 uses an internal clock. The farmduino comes with a 16Mhz external crystal which needs to be configured by writing the fuses in order to synchronize with atmega2560 also running 16Mhz. On the PCB the crystal is located at the lower left side of the atmega16U2 marked with designator *G2*. The crystal is the clock generator for the atmega16U2 for synchronizing events within the SoC.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2/crystal.png" width="500">
</a>

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
avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -U lfuse:w:0xff:m -U hfuse:w:0xd9:m -U efuse:w:0xf4:m
```

Additional parameters explained.
|Parameter|What it does|
|-|-|
|`-U`|says you like to deal with the fuses|
|`lfuse:w:0xff:m`|write LOW fuse with value `0xFF`|
|`hfuse:w:0xff:m`|write HIGH fuse with value `0xD9`|
|`efuse:w:0xff:m`|write EXTENDED fuse with value `0xF4`|

If all goes well *avrdude* will show a summary of the new fuse values.

## Programming
Please note, once the initial programming procedure is carried out successfully, the ATmega16U2 won't be recognized by the USB host (your PC) anymore. Instead it will transfer all messages between USB host and ATmega2560 back and forth. If for any reason this seems not possible, please see the troubleshooting section.

For programming atmeag16U2 open Flip, choose device and open the USB port. 

## Troubleshooting
To reset the firmware of Atmega16U2, there is an ISCP interface available on the PCB that can be connected to an IC programmer, e.g. Arduino UNO.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2/iscp-atmega16U2.png" width="500">
</a>
from genesis-USB.SchDoc

    D:\Program Files\Arduino\hardware\tools\avr\bin>avrdude.exe -C "D:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -c arduino -P COM3 -b 19200 -p m16u2 -vvv -U flash:w:"D:\Program Files\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\Arduino-COMBINED-dfu-usbserial-atmega16u2-Mega2560-Rev3.hex":i

Get configuration

    avrdude -p m16u2 -c wiring -P COM3 -C "D:\Program Files\Arduino/hardware/tools/avr/etc/avrdude.conf" -vvv -c avrisp -b 19200

write fuses


# Initial Programming of ATmega16U2
The ATmega16U2 serves as serializer between USB host and ATmega2560. The USB host may be your local PC at this time and later the Raspberry PI with FarmOS running on it. 

The SoC comes with the factory default firmware which won't act as serializer. You will need to update the firmware as described below, otherwise you won't be able to access ATmega2560 through USB.

## Electrical test
The USB-B port needs to be powered by connecting it to the local PC using an USB/B-to-USB/A cable. The USB circuit on the PCB is decoupled from all other circuits. Your PC will be USB host and the board the USB device. Power goes downstream from USB host to device.

Check wether or not the ATmega16U2 SoC is powered with the help of an oscilloscope. I use the Rigol DS1043Z. Connect the probe to the *VCC*, *AVCC* and *UVCC* pins, because all of them are powered through the USB-B power lines. The voltage level should be about 5V at each pin. If not, there is an issue with USB power supply.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2.png" width="500">
</a>

## Flashing the Firmware

### Driver installation
Use [Atmel Flip](https://www.microchip.com/en-us/development-tool/flip) software to connect to the ATmega16U2. I used Windows 11. Please note Flip requires a 32-bit Java JRE to start properly. Make sure Java binaries are added to PATH environment variables. 

If necessary install the Atmel USB driver *AtLibUsbDfu.dll* manually. It is located in *USB* directory of the Flip installation directory. Open Windows device manager and look for "unknown device". Right click the entry and select "update driver". Then select "search for driver on computer" and navigate to 

```bash
Your\Path\..\Atmel\Flip 3.4.7\usb
```

or where you installed Flip. Confirm the directory. The computer will find the correct driver and installs it. In the device manager the SoC is registered like here:

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/device-manager.png" width="500">
</a>

### First life signs

Open Flip and select *ATmega16U2* as device and *USB* as driver. Open the USB connection and the software will output some additional SoC data, such as hardware ID (signature bytes) and others. Do the *blank check* to verify the SoC is up and running.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/flip.png" width="500">
</a>

Use *avrdude* program to get a detailled list of current ATmega16U2 parameters. *Avrdude* ships with the official [Arduino IDE](https://www.arduino.cc/en/software). 

```bash
$> avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -b 115200
```

Commandline parameters explained
|Parameter|What it does|
|-|-|
|-p m16u2|the Atmel SoC that is addressed with the call, in this case ATmega16U2|
|-c wiring|protocol used for talking to Atmel SoC; wiring corresponds to STK500v2 internally which in turn is successor of STK500v1 and considered more stable|
|-P COM3|local communication port; here in Windows notation COM[n]|
|-C avrdude.conf|local path to avrdude configuration file|
|-vvv | verbose log of the communication with the SoC|
|-c avrisp|local PC is used as programmer|
|-b 115200|if local PC is programmer then 115200 is default; if programming is done through an Arduino instead (--> troubleshooting section), then it must be 19200 to work properly|
### Configure external crystal oscillator
By default the atmega16U2 uses an internal clock. The farmduino comes with a 16Mhz external crystal 

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/crystal.png" width="500">
</a>

```bash
avrdude -p m16u2 -c wiring -P COM3 -C "C:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -vvv -c avrisp -U lfuse:w:0xff:m -U hfuse:w:0xd9:m -U efuse:w:0xf4:m
```
### Programming
Please note, if the initial programming procedure is carried out successfully, the ATmega16U2 won't be recognized by the USB host (your PC) anymore. Instead it will transfer all those messages between USB host and ATmega2560 back and forth.

## Reset firmware to default
To reset the firmware of Atmega16U2, there is an ISCP interface available on the PCB that can be connected to an IC programmer, e.g. Arduino UNO.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/iscp-atmega16U2.png" width="500">
</a>
from genesis-USB.SchDoc

    D:\Program Files\Arduino\hardware\tools\avr\bin>avrdude.exe -C "D:\Program Files\Arduino\hardware\tools\avr\etc\avrdude.conf" -c arduino -P COM3 -b 19200 -p m16u2 -vvv -U flash:w:"D:\Program Files\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\Arduino-COMBINED-dfu-usbserial-atmega16u2-Mega2560-Rev3.hex":i

Get configuration

    avrdude -p m16u2 -c wiring -P COM3 -C "D:\Program Files\Arduino/hardware/tools/avr/etc/avrdude.conf" -vvv -c avrisp -b 19200

write fuses


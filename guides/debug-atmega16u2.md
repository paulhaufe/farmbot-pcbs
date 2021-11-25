# Setup ATmega16U2
On the Farmduino PCB the ATmega16U2 serves as serializer between USB and ATmega2560. The SoC comes with the factory default firmware which won't serve this purpose. You will need to update the firmware as described below.

## Electrical test
To test the ATmega16U2 SoC the USB-B port needs to be powered by connecting it to the local PC using an USB/B-to-USB/A cable. The USB circuit on the board is decoupled from all other circuits. Your PC will be USB host and the board the USB device. Power goes downstream from USB host to device.

Check wether or not the ATmega16U2 SoC is powered with the help of an oscilloscope. I use the Rigol DS1043Z. Connect the probe to the *VCC*, *AVCC* and *UVCC* pins, because at the end all of them are powered through the USB-B power line. The voltage level should be 5V at each pin. If not, there is an issue with USB power supply.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2.png" width="500">
</a>

## Retrieval of ATmega16U2 meta data
Use [Atmel Flip](https://www.microchip.com/en-us/development-tool/flip) software to connect to the ATmega16U2. I used Windows 11. Please note Flip requires a 32-bit Java JRE to start properly. Make sure Java binaries are added to the PATH environment variable. 

In my case it was necessary to install the Atmel USB driver *AtLibUsbDfu.dll* manually. It is located in *USB* directory of the Flip installation directory. Open Windows device manager and look for "unknown device". Right click the entry and select "update driver". Then select "search for driver on computer" and navigate to 

    *Your\Path\...\Atmel\Flip 3.4.7\usb* 

or where you installed Flip. Confirm the directory. The computer will find the correct driver and install it. In the device manager the Soc is registered like here:

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/device-manager.png" width="500">
</a>

Open Flip and select *ATmega16U2* as device and *USB* as driver. Open the USB connection and the software will output some additional SoC data, such as hardware ID (signature bytes) and others. Do the *blank check* to verify the SoC is up and running.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/flip.png" width="500">
</a>

## Firmware Update to setup ATmega2560
Please note, if the firmware update procedure is carried out successfully, the ATmega16U2 won't be recognized by the USB host (your PC) anymore. Instead it will transfer all those messages between USB host and ATmega2560 back and forth.

I installed the official [Arduino IDE](https://www.arduino.cc/en/software), because it comes with the right firmware for the ATmega16U2 already.

For the firmware update use Flip again. Please choose the correct device, open the USB connection and select *Program Target Device Memory* from the tools bar. You will be asked to provide the path to *.hex* firmware file. Navigate to the following path:

    *your-drive:\your-installation-directory\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\arduino-usbserial*

There is file named

    *Arduino-usbserial-atmega16u2-Mega2560-Rev3.hex*

Select it and apply the firmware update. If everything goes well, the device manager will recognize the ATmega2560 immediately, because the correct driver has been delivered and installed with Arduino IDE already.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega2560.png" width="500">
</a>
# Debug ATmega16U2
To test the ATmega16U2 the USB-B port needs to be powered by connecting it to the local PC using an USB/B-to-USB/A cable. The USB circuit on the board is decoupled from all other circuits. The PC will be USB host and the board the USB device. Power goes downstream from USB host to device.
## Electrical test
Check wether or not the ATmega16U2 SoC is powered with the help of an oscilloscope. I use the Rigol DS1043Z. Connect the probe to the *VCC*, *AVCC* and *UVCC* pins, because at the end all of them are powered through the USB-B power line. The voltage level should be 5V at each pin. If not there is an issue with USB power supply.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega16u2.png" width="500">
</a>

## Retrieval of Soc meta data
Use [Atmel Flip](https://www.microchip.com/en-us/development-tool/flip) software to connect to the ATmega16U2. I used Windows 11. Please note Flip requires a J32-bit Java JRE to start properly. Make sure Java binary is added to the PATH environment variable. 
In my case it was necessary to install the Atmel USB driver *AtLibUsbDfu.dll*. It is located in USB directory of the FLip installation directory. Open Windows device manager and look for "unknown device". Right click the entry and select "update driver". Then select "search for driver on computer" and
navigate to *Your\Path\...\Atmel\Flip 3.4.7\usb* or where you installed Flip. Confirm the directory. The computer will find the correct driver and install it. Flip will output some additional SoC data.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/flip.png" width="500">
</a>
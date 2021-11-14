# Debug ATmega16U2
To test the ATmega16U2 the USB-B port needs to be powered by connecting it to the local PC using an USB/B-to-USB/A cable. The USB circuit on the board is decoupled from all other circuits. The PC will be USB host and the board the USB device. Power goes downstream from USB host to device.
## Electrical test
Check wether or not the ATmega16U2 SoC is powered with the help of an oscilloscope. I use the Rigol DS1043Z. Connect the probe to the *VCC*, *AVCC* and *UVCC* pins, because at the end all of them are powered through the USB-B power line. The voltage level should be 5V at each pin.
![motors](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/atmega16u2.png)
# Initial Programming ATmega2560


I installed the official [Arduino IDE](https://www.arduino.cc/en/software), because it comes with the right firmware for the ATmega16U2 already.

For the firmware update use Flip again. Please choose the correct device, open the USB connection and select *Program Target Device Memory* from the tools bar. You will be asked to provide the path to *.hex* firmware file. Navigate to the following path within Arduino IDE installation directory:

    your\path\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\arduino-usbserial

There is file named

    Arduino-usbserial-atmega16u2-Mega2560-Rev3.hex

Select it and apply the firmware update. If everything goes well, the device manager will recognize the ATmega2560 immediately, because the correct driver has been delivered and installed with Arduino IDE already.

<a href="url"><img src="https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/guides/atmega2560.png" width="500">
</a>
# A guide to manufacture and program Farmduino by Farmbot on your own

Many thanks to the [FarmBot](https://farm.bot/) Team for making their great work publicly available as Open Source Hardware and Software. The [Farmduino](https://genesis.farm.bot/v1.5/Extras/bom/electronics-and-wiring#farmduino) device carries out all those commands by the Raspberry PI such as moving motors, reading sensors etc.

This guide tells you how to build an exact copy of the Farmduino v1.5 PCB (Printed Circuit Board) without being an expert in circuit design or electronics.

The whole procedure will take a few weeks due to manufacturing lead time, especially during times of global chip shortage. If this takes too long, [open an issue in this project](https://github.com/paulhaufe/farmbot-pcbs/issues) and leave me a message, I have a few left for private sale.

## 1. Manufacturing

If you order PCBA prototypes the first time, checkout the [general guideline](../README.md).

* [Manufacturing Notes for Farmduino PCBA](order.md)

## 2. Program Farmduino PCB

* [Setup of Power Supply](hardware-setup)
* [Initial programming of ATmega16U2](atmega16u2/readme.md)
* [Initial programming of ATmega2560](atmega2560/readme.md)
* Initital programming of STM32F303 (not yet available)
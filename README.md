# A guide to manufacture and program Farmduino by Farmbot on your own

Many thanks to the [FarmBot](https://farm.bot/) Team for making their great work publicly available as Open Source Hardware and Software. The [Farmduino](https://genesis.farm.bot/v1.5/Extras/bom/electronics-and-wiring#farmduino) device carries out all those commands by the Raspberry PI such as moving motors, reading sensors etc.

This guide tells you how to build an exact copy of the Farmduino v1.5 PCB (Printed Circuit Board) without being an expert in circuit design or electronics.

The whole procedure will take a few weeks due to manufacturing lead time, especially during times of global chip shortage. If this takes too long, [open an issue in this project](https://github.com/paulhaufe/farmduino-pcb-howto/issues) and leave me a message, I have a few left for private sale.

## 1. Print Farmduino Circuit Board

Small quantities of 5+ equipped PCB pieces are considered *PCB Assembly Prototypes* and are produced by literally hundreds of different PCB Manufacturers located in the Asian region.

* [Place an order for producing a Farmduino PCB Assembly prototype](/guides/place-pcb-order)
* [Manufacturing Notes for PCB Manufacturers](/guides/pcb-manufacturing/readme.md)

## 2. Program Farmduino PCB

* [Setup of Power Supply](/hardware/setup/hardware-setup.md)
* [Initial programming of ATmega16U2](/guides/atmega16u2/readme.md)
* [Initial programming of ATmega2560](/guides/atmega2560/readme.md)
* Initital programming of STM32F303 (not yet available)
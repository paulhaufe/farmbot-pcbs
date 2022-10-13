# Manufacturing of Farmbot PCB Assemblys

## 1. Prerequisites
Small quantities of 5+ equipped PCB pieces are considered *PCB Assembly Prototypes* and are produced by literally hundreds of different PCB Manufacturers located in the Asian region.

A typical PCB manufacturer from China or Taiwan expects the following files delivered together with an order. All manufacturing files for Farmbot PCBAs are saved in the respective folders of this repo.

* `Gerber files`, a standardised file format for description of PCB structures
* `BOM (Bill of Materials)`, list of all electronic components that shall be equipped on the PCB
* `Pick & Place file`, listing of the orientation of all electronic components
* a PDF copy of the manufacturing notes; [example of Farmduino notes](/farmduino/manufacturing-notes/readme.md)
* `Assembly Drawing` (optional), 3D drawing of the PCB from different perspectives
* `Schemes` (optional), copy of all circuit schemes for better understanding

Submitting assembly drawings and schemes is optional, because the are not necessarily needed for the technical manufacturing process, but should be provided to the engineers who are involved into the process anyway.

## 2. Order a PCB Assembly

The *PCB* (the raw boards without components fitted on), and the *Assembly* (the step of fitting the components to the board) will be ordered together.

1. Navigate to a PCB manufacturer`s website and select *PCB Assembly* from the main menu
2. Click on *Quote Now* or a similar button
3. Fill out the forms based on the values documented for each Farmbot PCBA in the project folders of this repo: [Farmduino](/farmduino/order.md), [Pi Adapter](/pi-adapter/order.md), 

## 3. Proceeed with the order

1. Click on `Calculate Now` to show the price estimate for PCB Assemblys.
2. Click on `Add to Cart`
3. Within the Cart page you are going to upload all mandatatory files (gerber, BOM, pick&place, Farmduino instructions)
4. You are being assigned an operator who reviews your uploads

Please wait until an operator reviews and confirms your uploads. You will be notified by E-Mail. In general the price is divided as follows.

* `cost of PCB`, the cost for the plane boards
* `cost of all components` of Farmduino; most prototype manufacturers order at [Digikey](https://www.digikey.com/) or [Mouser](https://mouser.com/) due to minimum order quantity of `1` component and high quality standards
* `assembly cost`; manual work of processing your order, setting up machines that do automatic pick & place, soldering, etc.
* `shipping cost`

Once confirmation is there and open issues adressed, you need to pay upfront :)
Depending on your location, country-specific taxes for clearing customs add up to the list. You will be notified by the ususal suspects such as DHL, UPS or FedEx.

## 4. Setup the PCB Assembly

There is still some things to do, such as firmware deployment for microcontrollers, cabling, trouble shooting etc. Check out the guidlines for the respective Farmbot PCBAs in the subfolders of this repo.
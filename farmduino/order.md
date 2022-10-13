# Manufacture Farmduino PCB Assembly

A typical PCB manufacturer from China or Taiwan expects the following files delivered together with an order. All files for Farmduino v1.5 are saved in this project folder, please see above.

* `Gerber files`, a standardised file format for description of PCB structures
* `BOM (Bill of Materials)`, list of all electronic components that shall be equipped on the PCB
* `Pick & Place file`, listing of the orientation of all electronic components
* a PDF copy of the [Manufacturing Notes of Farmduino](/guides/pcb-manufacturing/readme.md) page
* `Assembly Drawing` (optional), 3D drawing of the PCB from different perspectives
* `Schemes` (optional), copy of all circuit schemes for better understanding

Submitting assembly drawings and schemes is optional, because the are not necessarily needed for the technical manufacturing process, but should be provided to the engineers who are involved into the process anyway.

## Order Farmduino PCB Assembly

The *PCB* (the raw boards without components fitted on), and the *Assembly* (the step of fitting the components to the board) will be ordered together.

1. Navigate to a PCB manufacturer`s website and select *PCB Assembly* from the main menu
2. Click on *Quote Now* or a similar button
3. Fill out the forms according to the table below

### Manufacturing options for the PCB Assembly

The most important options are listed below. You might play around with the other options to enable more quality assurance or to comply with higher standards, which will result in higher price.

|Option|Value|Description|
|-|-|-|
|Manufacturing|`Turnkey`|The all inclusive option where you do not provide any parts to the manufacturer|
|Number of Components|`345`|The overall number of all electronic components|fitted on the PCB|
|SMDs|`311`|Total number of surface-mounted devices aka components|
|Through Holes|`34`|Total number of through-hole components|
|Unique parts|`73`|Total number umber of unique parts|
|BGA/QFP Parts|`8`| Total number of ICs with more than 16 pins (max. pin number vary); Farmduino has eight of them: 1xATmega16U2, 1xATmega2560, 1xSTM32F303x, 5xTMC2130x
|Assembly Side|`Single`|The Farmduino board is fitted on top side only|

### Manufacturing options for the PCB

The most important options are listed below. You might play around with the other options to enable more quality assurance or to comply with higher standards, which will result in higher price.

|Option|Value|Description|
|-|-|-|
|Layer Count|`4`|Amount of copper layers. 
|Layers|`TOP`,`GND`,`VCC` and `BOTTOM`|List of all copper layers from top to bottom
|Size|`134.366mm` x `105.5529mm`|Length and width of the board|
|Surface Finish|example: `Lead Free HASL`|The RoHS standard (*Restriction of Hazardous Substances Directive*) considers Lead as hazardous; it is not allowed to import a board containing Lead into the European Union; other countries have similar regulations|
|Material|`FR-4`| price-performance option|
|Thickness|`1.6`| standard thickness|
|Finished copper|`1 oz Cu`|price-performance option|

### Proceeed with the order

1. Click on `Calculate Now` to show the price estimate for PCB Assemblys.
2. Click on `Add to Cart`
3. Within the Cart page you are going to upload all mandatatory files (gerber, BOM, pick&place, Farmduino instructions)
4. You are being assigned an operator who reviews your uploads

Please wait until an operator reviews and confirms your uploads. You will be notified by E-Mail. In general the price is divided as follows.

* price of PCB, the cost for the plane boards
* price of all `345` components of Farmduino; most prototype manufacturers order at [Digikey](https://www.digikey.com/) or [Mouser](https://mouser.com/) due to minimum order quantity of `1` component and high quality standards
* Assembly cost; manual work of processing your order, setting up machines that do automatic pick & place, soldering, etc.
* shipping cost

5. Once confirmation is there and open issues adressed, you need to pay upfront :)
6. Depending on your location, country-specific taxes for clearing customs add up to the list. You will be notified by the ususal suspects such as DHL, UPS or FedEx.

Done.
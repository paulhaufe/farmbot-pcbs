# Manufacture Farmduino PCB Assembly

For the sake of simplicity [NextPCB](https://www.nextpcb.com/), a Chinese PCB Manufacturer, will serve as an example for placing an order. Typically a PCB manufacturer expects the following files delivered with an order.

All files for Farmduino v1.5 are saved in this project folder, please see above.

* `Gerber files`, a standardised file format for description of PCB structures
* `BOM (Bill of Materials)`, list of all electronic components that shall be equipped on the PCB
* `Pick & Place file`, listing of the orientation of all electronic components
* a PDF copy of the [Manufacturing Notes of Farmduino](/) page
* `Assembly Drawing` (optional), 3D drawing of the PCB from different perspectives
* `Schemes` (optional), copy of all circuit schemes for better understanding

Submitting assembly drawings and schemes is optional, because the are not necessarily needed for the technical manufacturing process, but should be provided to the engineers who are involved into the process anyway.

## Order Farmduino PCB Assembly

The *PCB* (the raw boards without components fitted on), and the *Assembly* (the step of fitting the components to the board) will be ordered together.

1. Open the [NextPCB](https://www.nextpcb.com/) website and select *PCB Assembly* from the main menu
2. Click on *Quote Now* and leave the other text input fields empty
3. Fill out the form according to the table below

### Manufacturing options for the PCB Assembly

The most important options are listed below, all other standard values are ok. You might play around with the other options to enable more quality assurance or to comply with higher standards, which will result in higher price.

|Option|Value|Description|
|-|-|-|
|Three Options|`Turnkey`|The all inclusive option where you do  not provide any parts to manufacturers factory|
|PCB Qunatity|`5`|Amount of pieces manufactured, I don't know of any low-budget PCB Prototype Manufacturer that produces just one piece
|Number of Components|`345`|The overall number of all electronic components fitted on the PCB|
|Assembly Side|`Single`|The Farmduino board is fitted on top side only

Some other vendors might ask for the numbers of SMD and Through-Holes components.

|Option|Value|Description|
|-|-|-|
|Number of SMDs|`311`|Amount of surface-mounted devices|
|Number of Through-Hole components|`34`|Amount of through-hole components|

### Manufacturing options for the PCB

The most important options are listed below, all other standard values are ok. You might play around with the other options to enable more quality assurance or to comply with higher standards, which will result in higher price.

|Option|Value|Description|
|-|-|-|
|Layer Count|`4`|Amount of copper layers. The layers from top to bottom are `TOP`,`GND`,`VCC` and `BOTTOM`
|Size|`134.366mm` x `105.5529mm`|length and width of the board
|Surface Finish|`Lead Free HASL`|The RoHS standard (*Restriction of Hazardous Substances Directive*) considers Lead as hazardous; it is not allowed to import a board with Lead into the European Union; other countries have similar regulations|

### Proceeed with the order

1. Click on `Calculate Now` to show the price estimate for 5 PCB Assemblys.
2. Click on `Add to Cart`
3. Now you need to add 
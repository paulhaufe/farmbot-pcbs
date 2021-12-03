# Manufacture Farmduino PCB Assembly

For the sake of simplicity [NextPCB](https://www.nextpcb.com/), a Chinese PCB Manufacturer, will serve as an example for placing an order. Typically a PCB manufacturer expects the following files delivered with an order.

All files for Farmduino v1.5 are saved in this project folder, please see above.

* `Gerber files`, a standardised file format for description of PCB structures
* `BOM (Bill of Materials)`, list of all electronic components that shall be equipped on the PCB
* `Pick & Place file`, listing of the orientation of all electronic components
* `Assembly Drawing` (optional), 3D drawing of the PCB from different perspectives
* `Schemes` (optional), copy of all circuit schemes for better understanding

Submitting assembly drawings and schemes is optional, because the are not necessarily needed for the technical manufacturing process, but should be provided to the engineers who are involved into the process anyway.

## Order Farmduino PCB Assembly

1. Open the [NextPCB](https://www.nextpcb.com/) website and select *PCB Assembly* from the main menu
2. Click on *Quote Now* and leave the other text input fields empty
3. Fill out the form according to the table below

Manufacturing options

|Option|Value|Description|
|-|-|-|
|Three Options|`Turnkey`|The all inclusive option where you do  not provide any parts|
|PCB Qunatity|`5`|Amount of pieces manufactured, I don't know of any low-budget PCB Prototype Manufacturer that produces just one piece
|Number of Components|`345`|The overall number of all electronic components fitted on the PCB|

# farmduino-pcb-howto
A guide to manufacture Farmduino device on your own
## Instruction for PCB assembly manufacturers
The gerber files do not contain designators for all through-hole components. That's why manufacturers will have a hard time to locate the correct location on the board for these components.

![Overview](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/overview.png "Overview")

### Encoder Headers
The encoder header designators P8, P9, P10, P11 match to the logical encoders Z, Y, X2, X1
* p8 -> Z ENCODER
* P9 -> Y ENCODER
* P10 -> X2 ENCODER
* P11 -> X1 ENCODER

![Encoders](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/p8-p9-p10-p11.png "Encoders")
### 12-pin header P17
The P17 header is located at the lower left corner of the board.
![12-pin header](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/p17.png "12-pin header")
### 4-pin motor headers X3..X7
The 4-pin headers X3, X4, X5, X6, X7 for connecting the stepper motors are located at the upper side of the board and match to the logical motor identifiers.
* X3 -> X2 MOTOR
* X4 -> AUX MOTOR
* X5 -> X1 MOTOR
* X6 -> Y MOTOR
* X7 -> Z MOTOR

![motors](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/x3-x4-x5-x6-x7.png "motors")
### 5-Pin UTM header
The 5-pin header with designator P2 is located at the lower bottom of the board.
![utm](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/p2.png "utm")
### 12-Pin header P20
The 12-pin header with designator P20 is located at the lower bottom of the board.
![utm](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/p20.png "utm")
### Fuse and fuse holder
The original Farmduino BOM lists *0287015.H* from *Littlefuse* as primary component for designator F1, but the two fuse blades do not fit to the four through-holes. The missing piece is a fuse holder that is soldered first. The fuse is put manually into the slot of the fuse holder, e.g. *3557-2* from *Keystone*.
1. Fuse F1
![fuse](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/f1.png "fuse")
2. Fuse holder
![fuse holder](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/f1-2.png "fuse holder")
## BOM
Please note, the following bill of materials (BOM) has not been tested with a real-world prototype. This warning will be replaced once tested successfully. The original Farmduino BOM does not qualify for manufacturing out-of-the-box and has been extended and changed at a few locations.

Line | Name | Description | Mount Technology | Designator | Quantity | Manufacturer 1 | Manufacturer Part Number 1 | Footprint
--- | --- | --- | --- | ---| ---| ---| --- | ---
1|TPS5430||SMT|D5|1|Texas Instruments|TPS5430DDA|SO-8-1||
2|0.02R,1%,1W,1206|Resistor|SMT|R74, R75, R76, R80, R81|5|||1206R||
3|0.22R,1%,1206|Resistor|SMT|R25, R26, R29, R30, R31, R32, R33, R71, R72, R73||10|||1206R||
4|1K,1%,0603|Resistor|SMT|R45, R46, R48, R106, R107, R112, R115, R116, R117, R119, R121, R122, R124, R125|14|||RC0603||
6|1M,1%,0603|Resistor|SMT|R18, R39|2|||RC0603||
7|1M,1%,1206|Resistor|SMT|R49|1|||RC1206||
8|1N4148|Default Diode|SMT|D1, D3, D4|3|MCC|1N4148WX-TP|SOD-323||
9|1NF,25V,0603|Capacitor|SMT|C16, C49, C69, C70, C71, C72, C73, C75, C121|9|||RC0603, 0603C||
10|1NF,50V,0603|Capacitor|SMT|C35, C36, C39, C40, C41, C42, C44, C50, C51, C52, C54, C56, C57, C59, C60, C67|16|||0603C||
11|1NF,1206,2000V|Capacitor|SMT|C28|1|KEMET|C1206C102KGRACTU|RC1206||
12|1UF,16V,0603|Capacitor|SMT|C58, C81, C82, C100, C104, C105, C106, C108, C111|9|||0603C||
13|2K,1%,0603|Resistor|SMT|R21, R22, R23, R35, R36, R37, R40, R41, R51, R59, R60, R61|12|||RC0603||
14|3X2P---2.54|Header, 3-Pin, Dual row|Through-Hole|X10, X12|2|||HDR2X3||
15|3.24K,1%,0603|Resistor|SMT|R78|1|||0603R||
16|4P---2.54|Header, 4-Pin|Through-Hole|P3, SWD1|2|||HDR1X4||
17|4X2P---2.54|Header, 4-Pin, Dual row|Through-Hole|P1, P6, P7|3|||HDR2X4||
18|4.7K,1%,0603|Resistor|SMT|R16, R17|2|||RC0603||
19|4.7NF,50V,0603|Capacitor|SMT|C15|1|||0603C||
20|5P---2.54|Header, 5-Pin|Through-Hole|P2|1|||HDR1X5||
21|6X2P---2.54|Header, 6-Pin, Dual row|Through-Hole|P4, P5, P19|3|||HDR2X6||
22|10K,1%,0603|Resistor|SMT|R1, R2, R3, R4, R5, R11, R12, R13, R14, R15, R20, R24, R27, R28, R34, R38, R47, R54, R56, R57, R58, R62, R63, R64, R65, R66, R67, R68, R70, R79|30|||RC0603, 0603R||
23|10R,1%,0603|Resistor|SMT|R6, R7, R8, R9, R10, R19, R42, R43, R44, R52, R53, R55|12|||RC0603||
24|10UF,10V,0603|Capacitor|SMT|C48, C122|2|||0603C, RC0603||
25|12P---2.54|Header, 12-Pin|Through-Hole|P20|1|||HDR1X12||
28|20K,1%,0603|Resistor|SMT|R50, R82, R85, R86, R88, R89, R92, R93, R94, R95, R98, R99, R100, R101, R104, R105, R118|17|||0603C, RC0603||
29|22NF,25V,0603|Capacitor|SMT|C34, C45, C90, C92, C93|5|||0603C||
30|22PF,25V,0603|Capacitor|SMT|C7, C22|2|||RC0603, 0603C||
31|22PF,50V,0603|Capacitor|SMT|C1, C4, C23, C24, C38|5|||RC0603||
32|22UH|Inductor|SMT|L1|1|Sumida|CDRH6D28NP-220NC|L7*7||
33|33K,1%,0603|Resistor|SMT|R69, R108, R109, R110, R111|5|||0603C, RC0603||
35|100K,1%,0603|Resistor|SMT|R77|1|||0603C||
36|100NF,25V,0603|Capacitor|SMT|C2, C3, C5, C6, C13, C17, C25, C26, C27, C29, C30, C31, C32, C33, C37, C46, C55, C63, C64, C65, C66, C68, C76, C89, C118|25|||RC0603, 0603C||
37|100NF,50V,0603|Capacitor|SMT|C14, C18, C47, C53, C61, C62, C74, C77, C78, C79, C80, C83, C84, C85, C86, C87, C88, C91, C94, C95, C96, C97, C98, C99, C101, C102, C103, C107, C109, C110, C112, C113, C114|33|||0603C||
38|100NF,50V,0805|Capacitor|SMT|C19, C20, C21|3|||0805C||
39|100PF,25V,0603|Capacitor|SMT|C115, C116, C117, C119, C120, C123, C124, C125, C126|9|||RC0603||
40|100R,1%,0603|Resistor|SMT|R114|1|||RC0603||
43|100UF,35V|Polarized Capacitor (Surface Mount)|SMT|C8, C9, C10, C11, C12|5|Panasonic|EEE-FN1V101XP|EC-5X5.3||
46|390R,1%,0603|Resistor|SMT|R83, R84, R90, R91, R96, R97, R102, R103|8|||0603C||
47|287015|Fuse|Through-Hole|F1|1|Keystone |3557-2|GF-C40|Littelfuse|0287015.H
48|ADUM1201||SMT|U9|1|Analog Devices|ADUM1201ARZ-RL7|SO-8N||
53|B180-13-F|Default Diode|SMT|V1, V2, V3, V4, V5|5|Diodes|B180-13-F|SMA||
54|B340A|Default Diode|SMT|V6|1|Diodes|B340A-13-F|SMA||
55|CG0603MLC-05E|Varistor (Voltage-Sensitive Resistor)|SMT|Z1, Z2|2|Bourns|CG0603MLC-05E|RC0603||
56|Header 7|Header, 7-Pin|Through-Hole|P8, P9, P10, P11|4|Molex|70543-0006|DIP-1*7-2.54||
57|IRFR3709ZTRPBF||SMT|M1, M2, M3, M4, M5|5|International Rectifier|IRFR3709ZTRPBF|DPAK||
58|LED,green,0603|Typical INFRARED GaAs LED|SMT|TX|1|||LED-0603||
60|LM324ADR|Quadruple Operational Amplifier|SMT|U17|1|ON Semiconductor|LM324ADR2G|SO-14||
63|miniASMDC050F-2|Thermal Fuse|SMT|F2|1|Littelfuse|MINIASMDC050F-2|RC1812||
64|Molex 43045-1212|Header, 12-Pin|Through-Hole|P17|1|Molex|43045-1212|43045-1212||
65|Molex 70543-0038|Header, 4-Pin|Through-Hole|X3, X4, X5, X6, X7|5|Molex|70543-0038|DIP-1*4-2.54||
67|P6SMBJ24CA|Schottky Diode|SMT|D2|1|Littelfuse|P6SMBJ24CA|SMB||
69|STM32F303CXT6||SMT|U14|1|STMicroelectronics|STM32F303CBT6|LQFP-48||
70|SW-PB|Switch|Through-Hole|S1|1|E-Switch|TL1105AF160Q|DIP6*6||
71|TLP185GB|4-Pin Phototransistor Optocoupler|SMT|U10|1|Toshiba|TLP185(GB-TPL,SE(T|SO-4||
72|TMC2130-LA(1)|IC STEPPER MOTOR DVR SPI 36QFN|SMT|U2, U3, U4, U5, U6|5|Trinamic|TMC2130-LA|QFN-36||
73|0.01UF, LOW ESR, X7R / X5R, 25V, 0603|Capacitor|SMT|C43|1|TDK|CGA3E2X7R1H103K080AA|RC0603||
75|100uF,6.3V,3528-21 (L x W x H)|Polarized Capacitor|SMT|E1, E4, E5|3|Kyocera AVX|TAJB107M006RNJ|3528-21, [NoValue]||
76|100uF,50V, Radial, 5mm pitch, 10mm diam.|Polarized Capacitor|Through-Hole|E2, E3|2|Panasonic|EEU-FC1H101|RB-.2X.4||
77|16Mhz, 32mm length x 25mm width|Crystal|SMT|G1, G2|2|Abracon|ABM8-16.000MHZ-B2-T|Y-3225||
78|LED,red,0603, 1.9V-2.4V, 20mA|Typical INFRARED GaAs LED|SMT|GRE1, RX|2|||LED-0603||
79|60R,100MHZ,0805|EMI Filter|SMT|L2, L3|2|Abracon|ACML-0805-600-T|0402-A, RC0805||
87|1K,1%,0603|Resistor Array, 4x0603|SMT|RP1, RP2, RP3, RP4, RP5, RP6|6|||603||
88|100R,1%,0603|Resistor Array, 4x0603|SMT|RP7|1|||603||
88|LED,green,0603,1.9V-2.4V,20mA|Typical INFRARED GaAs LED|SMT|AUX, LED1, LED2, LED3, LED4, LED5, RED6, X1, X2, Y, Z|11|||LED-0603||
90|Molex 151048-1209|Header, 2-Pin|Through-Hole|P12, P13, P14, P15, P16, X9|6|Molex|1510481209|151048||
91|ATMEG2560-16AU||SMT|U1|1|Microchip / Atmel|ATMEGA2560-16AU|LQFP-100||
92|ATMEGA16U2-MU||SMT|U8|1|Microchip / Atmel|ATMEGA16U2-MU|QFN-32||
93|AM26LS32||SMT|U7, U11|2|Texas Instruments|AM26LS32AID|SO-16-H||
95|LM358ADR||SMT|U12|1|ON Semiconductor|LM358ADR2G|SOIC-8||
96|AMS1117-3.3||SMT|U13|1|Advanced Monolithic Systems|AMS1117-3.3|SOT-223||
97|SN74AHCT1G125DBVR||SMT|U15|1|Texas Instruments|SN74AHCT1G125DBVR|SOT-23-5||
98|USB-A||Through-Hole|X8|1|TE Connectivity|17343661|USB-A180||
99|USB-B||Through-Hole|X11|1|TE Connectivity|5787834-1|USB-B180||

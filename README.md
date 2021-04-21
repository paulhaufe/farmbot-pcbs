# farmduino-pcb-howto
A guide to manufacture farmduino on your own
## Instruct the PCB manufacturer
The gerber files do not contain designators for all through-hole components. That's why manufacturers will have a hard time to locate the correct location on the board for these components.
### Encoder Headers
The encoder header designators P8, P9, P10, P11 match to the logical encoders Z, Y, X2, X1
* p8 -> Z Encoder
* P9 -> Y Encoder
* P10 -> X2 Encoder
* P11 -> X1 Encoder

![Encoders](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/p8-p9-p10-p11.png "Encoders")
### 12-pin header
The P17 header is located in the lower left corner of the board.
![Encoders](https://github.com/paulhaufe/farmduino-pcb-howto/blob/main/p17.png "Encoders")
# farmduino-pcb-howto
A guide to manufacture farmduino on your own
## Instruction for PCB assembly manufacturers
The gerber files do not contain designators for all through-hole components. That's why manufacturers will have a hard time to locate the correct location on the board for these components.
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
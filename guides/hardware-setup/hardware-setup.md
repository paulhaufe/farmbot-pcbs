# Hardware Setup

The following steps describe how to power the Farmduino device corectly. You will need a `24V DC / 150W power supply` with protective contact socket. For debugging purposes a programmable lab power supply is even better.

![crimping](/guides/hardware-setup/power-supply.png)

# Assemble power cable

The power cable is customized for the sole purpose of connecting the Farmduino to power through the red Molex connector with `X9` as designator. You are going to need a few items to succeed here.

|Item|Amount|Description|
|-|-|-|
|Outdoor Power Cable, 2 wires|1|cable standard `H07RN-F` or `SOOW`, 2x1.5mm², 1m for lab use (Farmbot in production will usually need more length)|
|Red Molex Receptable Housing|1|CP-6.5 Receptacle Housing, 6.50mm Pitch, Dual Row, Polarized, Positive Lock, 2 Circuits, Red </br>Molex part number [1510492209](https://www.molex.com/molex/products/part-detail/crimp_housings/1510492209)|
|Crimp Terminals|2|CP-6.5 Wire-to-Board Crimp Terminal, Female, 16-22 AWG</br>Molex part number [505978100](https://www.molex.com/molex/products/part-detail/crimp_terminals/0505978100)|
|Retainer|2|CP-6.5 Terminal Position Assurance (TPA) Retainer, 1 Circuit</br>Molex part number [511430105](https://www.molex.com/molex/products/part-detail/accessories/0511430105)|
|Crimp tool|1|Preferrably Hand Crimp Tool from Molex for 3.96mm Pitch Wire-to-Wire and 6.50mm Pitch Wire-to-Board Crimp Terminals, 16-20 AWG</br>Molex part number [638197600](https://www.molex.com/molex/products/part-detail/application_toolin/0638197600)|

Once you collected all the items from the list above, you can crimp the terminals onto the two wires with a crimp tool and plug them into the receptable housing. Don't forget to add the retainers as last step for stability.

Before:

![crimping](/guides/hardware-setup/crimping.png)

After:

![crimping](/guides/hardware-setup/power-board.png)

# Smoke test
Make sure the positive polarity connects to VCC (hot wire) and negative polarity to GND once plugged in. This is because the circuit is DC +24V which means it's a negative ground system. The Farmduino is powered using the Farmduino power cable with the red Molex connector. 

And now, power the device. If there is no smoke and the yellow power LED is on then it's all good so far.

Done.
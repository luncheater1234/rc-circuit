# rc-circuit

## **Our Project**

### **Final Circuits**
Transmitter Circuit:
![circuit (1)](https://user-images.githubusercontent.com/50378721/58183872-13b71580-7c7e-11e9-822c-e8fd2cdad8d2.png)

Receiver Circuit:
![circuit](https://user-images.githubusercontent.com/50378721/58183833-01d57280-7c7e-11e9-836e-00b2b7df7a67.png)

### **Components List**
- PT2262 Encoder
- Pt2272-M4 Decoder
- Transmitter module
- Reciever module
- IC 7805 voltage regulator (x2)
- 200k resistor
- 1.2M resistor
- 4x pcb switch
- 2x 9v battery
- battery lead off
- LED x6
- misc wires 
#### **Total Cost: $13.83**

## **RC Circut Building Process**
Power Supply:
For each circuit, we need a power supply. To make the power supply, use an ic 7805 voltage regulator. The voltage regulator takes the 9v from the battery and drops it to 5v, which is a usable voltage for the rf modules, encoder, and decoders. The ic 7805 has three prongs: one for the 9v input power, one ground, and one for the 5v output. These are shown below:

![Screen Shot 2019-05-22 at 2 15 11 PM](https://user-images.githubusercontent.com/50378721/58198315-090b7900-7c9c-11e9-8af9-347738e2aa53.png)

2 power supplies will be needed: one for the transmitter circuit and one for the receiver circuit.

Now, we learn how to make the transmitter circuit. Our Circuit diagram depicts how to wire the pt2262. Note the semi-circular indentation at the top indicating the orientation. The following are the definitions of the various pins: 

| Pin Name | Explanation |
| -------- | ------------ |
| A0-A7 |Extra input/output pins. Not connected to anything in our circuit |
| Vss | Ground |
| Vcc | Power in |
| DOUT | data output to transmitter module |
| OSC2/OSC1 | oscillator output -see more about finding the correct R values below |
| TE | Goes to ground |
| D0-3/A11-8 | data inputs- we connect to switches |

![PT2262](https://user-images.githubusercontent.com/50378721/58198126-bdf16600-7c9b-11e9-8742-f1fea20dd023.png)

The resistors needed to bridge the OSC2/OSC1 pins in the encoder and decoder can be determined from the following table:

| Pt2262 | Pt2272 | Voltage Range |
| ----- | ----- | ---- |
| 4.7MΩ | 820KΩ | 5-15V |
| 3.3MΩ | 680KΩ | 5-15V |
| 1.2MΩ | 200KΩ | 3-15V |

Depending on the voltage one plans to run the encoder and decoder at, the oscillator resistance must vary. The oscillator frequency of the pt2272 [The decoder we will discuss later] must be 2.5-8x the encoding pt2262. We used a 1.2MΩ resistor for our pt2262 and a 200KΩ resistor for our pt2272.


Depending on the voltage one plans to run the encoder and decoder at, the oscillator resistance must vary. The oscillator frequency of the pt2272 [The decoder we will discuss later] must be 2.5-8x the encoding pt2262. Suggested resistor values are:


## **Difficulties**
The main problems we encountered were with our voltage, buttons, resistors, led’s, breadboard, diodes, and transmitter chip. The first time our circuit did not work we assumed that had applied too high a voltage and were burning out our components. This turned out to be false, as we were using a 9V battery to power parts with power ratings of 5-15V. We continued to test all of our connections to ensure they had the correct amount of voltage until we discovered that the breadboard we were using had a break in connection in the middle of its power strips that was causing only half of our circuit to be powered. Upon moving to a different breadboard we were able to make one led light up using the circuits described above.




# **RC Circuit**

## **Overview**

Our goal was to create two circuits which could communicate with one another via radio waves. We initially wanted to use this to remotely control a car. However, we encountered so many problems that we downsized our goal to making a light bulb turn on and off on as dictated by a remote control. We used 4 lightbulbs, each remotely controlled by a switch. When a button is pressed the command is fed into an encoder. The encoder sends coded data to the transmitter module which then sends the command over FM radio waves to the receiver module in the receiver circuit. The receiver module of the receiver circuit feeds the data signal into a decoder, which then selectively powers the corresponding LED. 

![Blank Diagram](https://user-images.githubusercontent.com/50378721/58216160-328fc900-7ccb-11e9-9698-b7f123efc472.jpeg)

## **Final Circuits**
Transmitter Circuit:

![Screen Shot 2019-05-22 at 6 53 40 PM](https://user-images.githubusercontent.com/50378721/58214256-0ec88500-7cc3-11e9-8515-5040a6dd94ee.png)

Receiver Circuit:

![Screen Shot 2019-05-22 at 6 53 32 PM](https://user-images.githubusercontent.com/50378721/58214214-f22c4d00-7cc2-11e9-843f-4ac5be84f3ff.png)

### **Components List**
- PT2262 Encoder
- PT2272-M4 Decoder
- STX882 Transmitter Module
- SRX882 Reciever Module
- IC 7805 Voltage Regulator (x2)
- 200kΩ Resistor
- 1.2MΩ Resistor
- PCB Switch (x4)
- 9V Battery (x2)
- Battery Clip-on Lead Off (x2)
- LED (x5)
- Misc Wires 
#### **Total Cost: $13.83**

## **RC Circut Building Process**
### **Power Supply:**
Two power supplies will be needed; one for the transmitter circuit and one for the receiver circuit. To make the power supplies, use an IC 7805 voltage regulator. The voltage regulator takes 9V from the battery and drops it to 5V, which is a usable voltage for the RF modules, encoder, and decoder. The IC 7805 has three prongs: one for the incomong 9V, one connected to ground, and one for the 5V output. These are shown below:

![Screen Shot 2019-05-22 at 2 15 11 PM](https://user-images.githubusercontent.com/50378721/58198315-090b7900-7c9c-11e9-8af9-347738e2aa53.png)

### **Transmitter Circuit**

Our Circuit diagram depicts how to wire the PT2262. Note the semi-circular indentation at the top indicating the orientation. The following are the definitions of the various pins: 

| Pin Name | Function |
| -------- | ------------ |
| A0-A7 |Input/output pins (not used in our circuit) |
| Vss | Ground |
| Vcc | Power input |
| DOUT | Data output to transmitter module |
| OSC2/OSC1 | Oscillator output -see more about finding the correct R values below |
| TE | Goes to ground |
| D0-3/A11-8 | Data inputs- we connect to switches |

![PT2262](https://user-images.githubusercontent.com/50378721/58198126-bdf16600-7c9b-11e9-8742-f1fea20dd023.png)

The resistor values needed to bridge the OSC2/OSC1 pins in the encoder and decoder can be determined from the following table:

| PT2262 | PT2272 | Voltage Range |
| ----- | ----- | ---- |
| 4.7MΩ | 820KΩ | 5-15V |
| 3.3MΩ | 680KΩ | 5-15V |
| 1.2MΩ | 200KΩ | 3-15V |

Depending on the voltage one plans to run the encoder and decoder at, the oscillator resistance must vary. The oscillation frequency of the PT2272 must be 2.5 to 8 times that of the encoding PT2262. The magnitude of the frequency of the oscilator has an inverse relationship with the resistance used, so the PT2262 must always have the larger resistor. We used a 1.2MΩ resistor for our PT2262 and a 200KΩ resistor for our PT2272.

Next, wire the transmitter module as shown in the image below:

![Screen Shot 2019-05-22 at 2 33 27 PM](https://user-images.githubusercontent.com/50378721/58199501-994abd80-7c9e-11e9-9a72-bfe49558a173.png)

| Pin Name | Function | 
| --- | --- |
| 1 | ANT: antena attachment |
|2 | DATA: Data input from DOUT of encoder|
| 3 | VCC: power input from IC 7805 voltage regulator|
| 4 | GND: ground, which is connected to the negative battery terminal |

Finally, each component is connected as shown in our transmitter circuit diagram.

### **Receiver Circuit**

First, build the second power supply identically to the first. Then, connect the decoder and receiver modules. The purpose of the decoder is to take the signals detected by the receiver and decode them so they can perform functions. Here we are using them to turn on and off LED lights. The following is a pin diagram of the PT2272:

![Screen Shot 2019-05-22 at 2 46 44 PM](https://user-images.githubusercontent.com/50378721/58200276-70c3c300-7ca0-11e9-8747-6cedb8897f48.png)

The pins of the PT2272 connect as follows: 

| Pin Name | Function |
| --- | --- |
| A0-A7 | Outputs (not used) |
| VSS | Ground |
| VCC | 5V power supply |
| VT | Valid Transmission: powered whenever a signal is received |
| OSC1/OSC2 | Oscillators: connected by resistors, see the resistance values above |
| DIN | Data in: comes from both outputs of receiver module |
| A11-A8 | Data out: connected to LED which indicate a signal was received |

The next component to wire is the receiver module:

![Screen Shot 2019-05-22 at 2 53 09 PM](https://user-images.githubusercontent.com/50378721/58203003-1712c700-7ca7-11e9-923e-7da11abd4b3a.png)

The pins of the receiver module connect as described:

| Pin Name | Function |
| --- | --- |
| 1 | ANT: antenna |
| 2 | GND: connect to ground aka negative battery terminal |
| 3 | VCC: connect to IC 7805 circuit to power reveiver |
| 4 | CS: connect to DIN of decoder to indicate when a signal is received |
| 5 | DATA: connect to DIN of encoder, same place as CS |
| 6 | GND: connect to negative battery terminal |
| 7 | ANT: optional other antena that does not need to be connected |

To finish connect the components in the receiver circuit as shown in the wiring diagrams above. 

## **Debugging**

Steps to take if your lightbulbs do not light up when the buttons are pressed:

- Use a multimeter to check that there is no connection between the ground and the power supply. If there is, something has shorted. You will need to go back and check all of your connections.

- Check with the multimeter that everything is connected how it should be: Are your switches and LED lights connected to ground? If you are using a breadboard, is your entire circuit connected to power? Some breadboards have power strips that are disconnected in the middle. 

- Make sure that the switches are oriented in the correct direction. The ground and power wires should be connected with the button's legs pointed towards them, not away. If this is unclear, an easy way to test for the correct orientation is to wire up a simple circuit with just a switch, LED, and power supply. You can follow the circuit diagram below:



- Ensure your circuit is getting the correct amount of power. The encoder and decoder are rated for between 3 and 15V, depending on what resistance you use in the oscillators. However, the transmitter and receiver modules are only rated until about 5.5V. It is important to supply a voltage that falls inside the 3-5.5V range. 

- If you can't find the cause of your troubles, wire up a debugging circuit which bypasses the transmitter and receiver module. Essentially, wire everything as normal, but leave the transmitter and receiver out, merely connecting the DOUT of the encoder to the DIN of the decoder. Below is the wiring diagram we used. 



- If the circuit still doesn't work, repeat steps 1-4 in the debugging circuit until it works. 

### **Good Luck!**


# ECE482_FA23
UIUC ECE 482 - Digital IC Design Final Project Repository

## Project Purpose
In this project, we design a 16:1 serializer and a 1:16 deserializer in a 45-nm CMOS technology. We also design a pseudo-random bit sequence (PRBS) generator circuit; that provides the test data for our circuit.

## DEMUX
The 1:2 DEMUX folder includes schematic, symbol, and layout folders. The output of the serializer is connected to the 1:2 DEMUX in our circuit where one of the outputs is connected to the input of the deserializer and the other output is terminated by a 20-fF capacitor, emulating the actual circuitry that would be placed there. This allows the serializer to operate in loopback mode. The control signal for the demultiplexer is EXT-TX, an active-high 1.8-V signal fed in from off-chip. When EXT-TX = 0, the circuit is in loopback mode, and the serializer output is directed back to its input through the demultiplexer. 

## MUX
The 2:1 MUX folder includes schematic, symbol, and layout folders. The 2:1 MUX is used to select what to output to the input of the deserializer. When EXT-TX = 1, the MUX outputs the "real" serial data. When EXT-TX = 0, the MUX takes in the loopback data from the serializer. 

## SER_MUX
The SER_MUX folder includes schematic, symbol, and layout folders. This MUX is used inside the serializer and is the same MUX used in the MUX folder, but is laid out differently THe MUX is used to select between two streams of data. 

## integration/schematic
The integration/schematic includes the final schematic, symbol, and layout folders. Our complete implemented circuit is in this folder. 

## VSS_VIA/layout
The VSS_VIA/layout folder includes the layout folder for the VSS via.

## VDD_VIA/layout
The VDD_VIA/layout folder includes the layout folder for the VDD via. 

## SER_TransmissionGate
The SER_TransmissionGate folder includes the final schematic, symbol, and layout folders. This folder includes all the necessary components to implement a transmission gate used in the serializer.

## SER_Inverter
The SER_Inverter folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement an inverter that is used in the serializer. 

## SER_Dflipflop
The SER-Dflipflop folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement a Dflipflop that is used in the serializer. The Dflipflops allow the data to be held temporarily and then serialized through the MUX which switches from selecting between the two streams of data.

## SER_2to1_Serializer
The SER_2to1_Serializer folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement a 16:1 serializer. The 2:1 Serializer is cascaded into many levels to implement the 16:1 serializer.

## SERDES_OffChipBuffer
The SERDES_OffChipBuffer folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement an off-chip buffer for the circuit. The inverter is used to drive anything that is off the chip. 

## SCHMITT_BUFFER_1p8V_GIVEN
The SCHMITT_BUFFER_1p8V_GIVEN folder includes schematic, symbol, and layout folders. This folder is given to use from the 482 starter project files. The EN and EXT-TX signal for the PBRS generator is routed through the Schmitt Trigger Buffer. 

## PBRS_XOR
The SCHMITT_BUFFER_1p8V_GIVEN folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement an XOR gate in the PBRS. XOR gates, in collaboration with shift registers, are utilized to create pseudo-random sequences.

## PBRS_TSPC_REGISTER
The PBRS_TSPC_REGISTER folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement True single-phase clock (TSPC) shift registers. These registers are employed in collaboration with XOR gates to generate pseudo-random sequences.

## PBRS_OR
The PBRS_OR folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement OR gates used in the PBRS. These OR gates are used to implement the EN signal in the PBRS.

## PBRS_NOR
The PBRS_NOR folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement NOR gates used in the PBRS.

## PBRS_Inverter
The PBRS_Inverter folder includes schematic, symbol, and layout folders. This folder includes all the necessary components to implement inverter gates used in the PBRS. 

## CLK_BUFFER_GIVEN:
This is the provided CLK buffer file, it buffers the clock signal from the input to the rest of the circuit.


## DESEAR_COM:
This is the toplevel deserializer it performs the full functionality. It converts a serial data line into 16 seperate data lines
Inputs: FCLK which is the 1600 MHz clock; SCLK which is the 100 MHz clock; DATAIN which is the serial data stream;
Outputs: FCLKBAR which is the 1600 MHz clock but inverted; P1-P16 which is the 16 data stream outputs
IO: VDD which is power; VSS which is ground

## DESER_Bottom:
This is the bottom half of the desearilizer, which contains 16 registers and creates 16 temporary data stream outputs cycling based on the 1600 MHz frequency
Inputs: DATAIN which is the serialized datastream; CLK which is the 1600 MHz clock; CLKBAR which is the 1600MHz clock but inverted
Outputs: O1-O16 which are the temporary data stream outputs
IO: VDD which is power; VSS which is ground

## DESER_Top:
This is the top half of the desearilizer, which contains the 16 registers which ensures that the outputs are cycled based on the 100 MHz frequency
Inputs: CLK which is the 100 MHz clock; CLKBAR which is the 100 MHz clock but inverted; O1-O16 which is the 16 temporary data stream outputs from DESER_Bottom
Outputs: P1-P16 which are the 16 data stream outputs on the 100 MHz cycle
IO: VDD which is power; VSS which is ground

## DESER_Register:
This is the register used in the desearilizer design, it is comprised of 2 transmission gates and 2 inverters. It samples data on the posedge of CLK.
Inputs: D which is the data; CLK which is the clock; CLKBAR which is the clock but inverted
Outputs: Q which is the sampled data
IO: VDD which is power; VSS which is ground

## DESER_CLKDIV2:
This is a frequency divider by 2, it uses DESER_Register.
Inputs: CLK which is the input clock at frequency f; CLKBAR which is the inverted input clock at frequency f
Outputs: CLKOUT which is the output clock at frequency f/2; CLKBAROUT which is the inverted output clock at frequency f/2
IO: VDD which is power; VSS which is ground

## DESER_CLKDIV4:
This is a frequency divider by 4, it uses DESER_CLKDIV2.
Inputs: CLK which is the input clock at frequency f; CLKBAR which is the inverted input clock at frequency f
Outputs: CLKOUT which is the output clock at frequency f/4; CLKBAROUT which is the inverted output clock at frequency f/4
IO: VDD which is power; VSS which is ground

## DESER_CLKDIV8:
This is a frequency divider by 8, it uses DESER_CLKDIV2.
Inputs: CLK which is the input clock at frequency f; CLKBAR which is the inverted input clock at frequency f
Outputs: CLKOUT which is the output clock at frequency f/8; CLKBAROUT which is the inverted output clock at frequency f/8
IO: VDD which is power; VSS which is ground

## DESER_CLKDIV16:
This is a frequency divider by 16, it uses DESER_CLKDIV2.
Inputs: CLK which is the input clock at frequency f; CLKBAR which is the inverted input clock at frequency f
Outputs: CLKOUT which is the output clock at frequency f/16; CLKBAROUT which is the inverted output clock at frequency f/16
IO: VDD which is power; VSS which is ground

## DESER_Inverter_1:
This is a size 1 inverted used in the Register.
Inputs: IN which is the input signal
Outputs: OUT which is the inverted IN
IO: VDD which is power; VSS which is ground

## DESER_Inverter_32:
This is a size 32 inverted used in DESEAR_COM.
Inputs: IN which is the signal to be ineverted
Outputs: OUT which is the inverted signal
IO: VDD which is power; VSS which is ground

## DESER_TransmissionGate_1:
This is the first transmission gate used in DESER_Register, this enables the signal to passthrough when CLK is low.
Inputs: IN which is the signal to be transmitted
Outputs: OUT which is the transmitted signal
IO: VDD which is power; VSS which is ground

## DESER_TransmissionGate_2:
This is the first transmission gate used in DESER_Register, this enables the signal to passthrough when CLK is high.
Inputs: IN which is the signal to be transmitted
Outputs: OUT which is the transmitted signal
IO: VDD which is power; VSS which is ground

## PRBS:
This is the toplevel PRBS which performs full functionality. During a posedge of the EN it sets all output registers to signal high.
Inputs: EN which controls the PRBS dictating when it should start; CLK which is the 100 MHz signal
Outputs: Q0-Q15 which is the output signals of the PRBS
IO: VDD which is power; VSS which is ground

## LVLSHIFTER_DOWN:
This is the toplevel for the level-shifter down. It transforms a voltage from 1.8V to 1.1V
IO: VDD is the 1.1V power; VDDIO is the 1.8V power; VSS is ground; IN is the 1.8V signal; OUT is the 1.1V signal; OUTBAR is the logical negative of OUT

## LVLSHIFTER_UP:
This is the toplevel for the level-shifter up. It transforms a voltage from 1.1V to 1.8V
IO: VDD is the 1.1V power; VDDIO is the 1.8V power; VSS is ground; IN is the 1.1V signal; OUT is the 1.8V signal; OUTBAR is the logical negative of OUT













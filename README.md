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









# SERDES: T871 DESERIALIZER

## Overview:
This is the submission of the VHDL Qualification Task 871 A to apertus° Association.

Module Structure is as following:  
serdes_top.vhd ------------Top-Module  
|--> serializer.vhd ----------Parallel to Serial converter  
|--> deserializer.vhd ------Serial to Parallel converter  

A test bench named serdes_top_tb.vhd has been provided for simulating the design.  

User Contraints file master.ucf is located in ise project folder.  
The source VHDL files are contained in src/ and also they are linked to the Xilinx ISE 14.7 Project in ise/.

The cfg/ contains configuration of all the compilation tools.  
The folder Simulation Results contains the VCD file and screenshots of post route simulation of the design on Zynq 7020 with 100 MHz input clock.

## Usage: 
This project contains makefile for terminal based compilation.  
_Command_ : $ make  &lt;option&gt; 

The makefile has been provided with following options:  
1) all    :  Default Option. Compilation, post-route simulation and launches the ISIM simulator GUI.
2) synth  :  Synthesis of the top module. 
3) map    :  Mapping the design.
4) par    :  Placement and routing of design. 
5) timing :  Generating timing.
6) netgen :  Generating netlist.
7) fuse   :  Generating post route simulation model.
8) sim    :  Launching simulation in ISIM GUI.
9) report :  Viewing Design Summary and report.
10) ise   :  Launching Xilinx ISE project in Project Navigator. 
11) clean :  Cleaning the build.

## Task Approach:
The top module takes input clock of 100 MHz from the top test bench module. This clock is then fed to a PLL through a BUFG for generation of 300 MHz 0° and -75° clock. The -75° clock serves as a bit clock for deserializer. The 300 MHz 0° is fed to the PISO shift register and DDR sampling registers in serializer.vhd. The serializer samples the data at both edge of the clock and sends a rising pulse at ready pin when it is available to sample a new data word. The 300 MHz -75° is fed to DDR sampling registers and the SIPO shift register in deserializer.vhd 
3 different word size have been provided here which are selected by help of depth selection input lines in serializer.vhd and deserializer.vhd. "00" -> 8-bit | "01" -> 10-bit | "10" -> 12-bit mode.   
DDR register construct has been made at the link ends to double the data transfer rate.  
Link training has been implemented by using a Test Pattern 0xBAF (truncated for lower bit modes). This pattern is sent by the serializer initially when the link is not trained. As soons as the deserializer synchronisizes with the the serializer, it reverts a active-high in the link trained signal to serializer. From here the actual data transmission starts at 50Msps for 12bit, 60Msps for 10bit and 75Msps for 8bit.


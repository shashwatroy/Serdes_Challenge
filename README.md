# SERDES: T871 DESERIALIZER

## Overview:
This is the submission of the VHDL Qualification Task 871 A to apertus° Association.

Module Structure is as following:  
serdes_top.vhd ---------------Top-Module  
|--> serializer.vhd ----------Parallel to Serial converter  
|--> deserializer.vhd --------Serial to Parallel converter  

A test bench named serdes_top_tb.vhd has been provided for simulating the design.  

User Contraints file master.ucf is located in ise project folder.  
The source VHDL files are contained in src/ and also they are linked to the Xilinx ISE 14.7 Project in ise/.

The cfg/ contains configuration of all the compilation tools.  

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

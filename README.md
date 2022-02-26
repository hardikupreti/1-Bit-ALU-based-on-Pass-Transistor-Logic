# 1-Bit-ALU-based-on-Pass-Transistor-Logic

This repository presents the design of a 1 Bit ALU designed using Pass Transistor Logic. A 10T design has been implemented using Synopsis Custom Compiler on 28nm CMOS Technology.

# Table of Contents
   * [Abstract](#abstract)
  * [Reference Circuit Details](#reference-circuit-details)
  * [Reference Circuit Diagram](#reference-circuit-diagram)
  * [Reference Waveform](#reference-circuit-waveform)
- [Simulation in Synopsys Custom Compiler](#simulation-in-synopsys)
  * [Schematic](#schematic)
  * [Symbol](#symbol)
  * [Testbench](#Testbench)
  * [Parameters for DC Voltage Source for VDD](#Parameters-for-DC-Voltage-Source-for-VDD)
  * [Parameters for Pulse Voltage Sources for inputs](#Parameters-for-Pulse-Voltage-Sources-for-inputs)
  * [Transient Settings](#transient-settings)
  * [Netlist](#netlist)
  * [Waveform](#waveform)
  * [Conclusion](#conclusion)
  * [Acknowledgement](#acknowlegement)
  * [References](#references)


## Abstract

A Pass Transistor Logic-based 1 Bit 
ALU has been presented consisting of 10T. Reuse of adder
hardware has been done to reduce the count of transistors for 
implementing the circuit. A Low power 6T-based 1 Bit Full 
Adder circuit has been designed and XOR operation has been 
derived from the same hardware. AND, OR have been implemented separately. The reference paper has utilized 65 nm 
CMOS technology helps to attain lower Power and Area consumption[1].

## Reference Circuit Details

A. 1 Bit Full Adder Circuit

In the design, Pass Transistor-based MUX are fed with 
XOR of a and b to select the output to be obtained from the 
Sum and the Carry pins.

The circuit of the Full Adder is shown below:
<p align="center">
<img src="Images/1bitfulladder_ref.jpeg"></br>
  Fig. 1: 1 Bit Full Adder Reference Circuit [2]
</p>



## Reference Circuit Diagram
The circuit schematic of the ALU is shown below
<p align="center">
<img src="design/ALU_ref.jpeg"></br>
  Fig. 1: Reference ALU Circuit [1]
</p>

## Reference Circuit Waveform
<p align="center">
<img src="design/waveform_ref.jpeg"></br>
  Fig. 2: Reference Waveform [1]
</p>

# Simulation in Synopsys
## ALU Schematic
<p align="center">
<img src="design/ALUdesign.png"></br>
  Fig. 3: ALU Schematic using Pass Transistor Logic
</p>

## Symbol
<p align="center">
<img src="design/ALUsymbol.png"></br>
  Fig. 4: ALU Symbol 
</p>

## Testbench
<p align="center">
<img src="design/ALU_tb.png"></br>
  Fig. 5: Testbench for ALU 
</p>

## Parameters for Pulse Voltage Sources for Inputs
<p align="center">
<img src="design/inputs.png"></br>
  Fig. 5: DC VDD and Pulse Voltage Inputs 
</p>


## Transient Settings
<p align="center">
<img src="design/transient.png"></br>
  Fig. 9: The Transient Analysis inputs Run at 5ns step with stop time 100ns 
</p>

## Netlist
```
*  Generated for: PrimeSim
*  Design library name: sm_hvt_levelshifter
*  Design cell name: hvt_levelshifter_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Wed Feb 23 02:17:30 2022

.global gnd!
********************************************************************************
* Library          : sm_hvt_levelshifter
* Cell             : hvt_levelshifter
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt hvt_levelshifter gnd_1 out vddh vddl vin
xm8 net85 net94 gnd_1 gnd_1 n105 w=0.1u l=0.03u nf=1 m=1
xm7 net83 vin gnd_1 gnd_1 n105 w=0.1u l=0.03u nf=1 m=1
xm6 net43 net44 net85 gnd_1 n105 w=0.1u l=0.03u nf=1 m=1
xm5 net39 net44 net83 gnd_1 n105 w=0.1u l=0.03u nf=1 m=1
xm4 out net103 net19 net44 n105 w=0.1u l=0.03u nf=1 m=1
xm3 net19 net51 net44 net44 n105 w=0.1u l=0.03u nf=1 m=1
xm2 net9 out net44 net44 n105 w=0.1u l=0.03u nf=1 m=1
xm1 net51 net63 net9 net44 n105 w=0.1u l=0.03u nf=1 m=1
xm0 net94 vin gnd_1 gnd_1 n105 w=0.1u l=0.03u nf=1 m=1
xm15 net63 net103 vddh vddh p105 w=0.1u l=0.03u nf=1 m=1
xm14 net103 net63 vddh vddh p105 w=0.1u l=0.03u nf=1 m=1
xm13 out net103 vddh vddh p105 w=0.1u l=0.03u nf=1 m=1
xm12 net51 net63 vddh vddh p105 w=0.1u l=0.03u nf=1 m=1
xm11 net94 vin vddl vddl p105 w=0.1u l=0.03u nf=1 m=1
xm10 net43 net44 net63 vddh p105 w=0.1u l=0.03u nf=1 m=1
xm9 net39 net44 net103 vddh p105 w=0.1u l=0.03u nf=1 m=1
vbias net44 gnd! dc=0.6
.ends hvt_levelshifter

********************************************************************************
* Library          : sm_hvt_levelshifter
* Cell             : hvt_levelshifter_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 gnd! out net8 net6 net10 hvt_levelshifter
v6 net8 gnd! dc=3.3
v5 net6 gnd! dc=1.05
v9 net10 gnd! dc=1.05 pulse ( 0 1.05 0 0.1u 0.1u 5u 10u )








.tran '1u' '30u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(out) v(net10)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end

```
## Waveform

<p align="center">
<img src="design/ALUwaveform.png"></br>
  Fig. 11: ALU Waveform 
</p>

## Conclusion
A 1 Bit ALU has been designed on the Synopsys Custom Compiler and the waveform has been obtained. The use of Pass Transistor Logic helps to greatly bring down the number of transistors to 10 transistors. Also, due to less number of transistors, the Area, as well as the power consumption of this design, is less as compared to the earlier designs of ALU which have more transistors.

## Acknowledgement
1. Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com
2. Chinmay panda, IIT Hyderabad
3. Sameer Durgoji, NIT Karnataka
## References
[1]. G. Karthik Reddy, Kavita Khare, " Low power-area 
designs of 1-bit full adder in cadence virtuoso platform," 
International Journal of VLSI design & Communication 
Systems (VLSICS) VolA, NoA, August 2013.

[2]. G. K. Reddy, "Low power-area Pass Transistor Logic 
based ALU design using low power full adder design," 2015 
IEEE 9th International Conference on Intelligent Systems and 
Control (ISCO), 2015,

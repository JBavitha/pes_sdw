# Mealy Sequence Detector (1010 without Overlap)
This repository contains the source code and documentation for a Mealy state machine-based sequence detector designed to recognize the pattern "1010" without overlap in an input sequence. This project provides a clear example of how to design and implement a Mealy finite state machine (FSM) for sequential pattern detection.

## Overview
A Mealy state machine is a type of finite state machine where the outputs are dependent on both the current state and the current input. In this project, we've implemented a Mealy state machine to detect the sequence "1010" in an input stream. The detector recognizes the sequence without allowing for overlap, meaning that once the "1010" sequence is detected, it won't immediately recognize it again until another "1" is encountered.

## State Diagram

1010 Non-overlapping Mealy Sequence detector



![image](https://github.com/JBavitha/pes_sdw/assets/142578450/f5ad4b29-5984-475b-8d80-4b01c9a8a05a)

## Application
- Data Communication
- Network Security
- Industrial Automation
- Pattern Recognition
- Firmware and Embedded Systems


## Tools Used in RTL to GLS flow are:

1.iVerilog:
- A free and open-source Verilog simulation and synthesis tool.
- Part of the Icarus Verilog project.
- Utilized for simulating Verilog hardware description language code.
- It enables testing the design using a test bench, which applies stimulus to verify the functionality.
- Monitors input changes and evaluates corresponding output responses.

2.GTKwave:
- A free and open-source waveform viewer.
- Mainly used for visualizing simulation results produced by digital simulation tools such as Icarus Verilog.

3.Yosys:
- An open-source framework designed for Verilog RTL synthesis.
- Widely employed in digital design for converting high-level digital circuit descriptions into gate-level representations.
- Helps transform behavioral descriptions (e.g., Verilog code) into netlists, offering detailed information about the digital logic through gates and their connections.

## Functional Simulation 

To clone the repository use the below command 

```
git clone https://github.com/JBavitha/pes_sdw
```
Both the Verilog code and its corresponding testbench are loaded into the iVerilog tool.

```
vim pes_sdw.v
vim pes_sdw_tb.v
iverilog pes_sdw.v pes_sdw_tb.v
./a.out
gtkwave pes_sdw_tb.vcd

```



![Screenshot from 2023-10-21 14-52-18](https://github.com/JBavitha/pes_sdw/assets/142578450/04683d8c-aa6f-4e6e-bf60-8132f97c132b)

![Screenshot from 2023-10-21 14-44-18](https://github.com/JBavitha/pes_sdw/assets/142578450/57f07cdd-1fef-4f94-9798-419b74aaefe5)

![Screenshot from 2023-10-21 14-48-49](https://github.com/JBavitha/pes_sdw/assets/142578450/5211fbae-fc20-473e-970b-e123fad6ed2d)


**Pre synthesis Simulation result**

![Screenshot from 2023-10-21 11-54-46](https://github.com/JBavitha/pes_sdw/assets/142578450/a64737bc-8af7-4df3-9c0a-0655fd25f444)


## RTL Synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog pes_sdw.v
synth -top pes_sdw

```

![image](https://github.com/JBavitha/pes_sdw/assets/142578450/15f08c25-f610-42f1-bcd6-214167712107)

![image](https://github.com/JBavitha/pes_sdw/assets/142578450/e5f4cf9e-1d4a-4340-862c-c248de42372c)


To view the netlist

```
 abc -liberty -lib ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 show

```

![Screenshot from 2023-10-21 12-02-53](https://github.com/JBavitha/pes_sdw/assets/142578450/62757a48-a0c2-4591-bf99-94b2914cd310)

To get .net 
```
write_verilog pes_sdw_net.v
!vim pes_sdw_net.v

```

![image](https://github.com/JBavitha/pes_sdw/assets/142578450/4df29d9c-a985-463b-85f8-0a38ab7649e6)


![image](https://github.com/JBavitha/pes_sdw/assets/142578450/c20a5362-86d0-4e69-9e62-65c9db06bc22)


To get even more simpler code type the following commands 

```
write_verilog -noattr pes_sdw_net.v
!vim pes_sdw_net.v

```

![image](https://github.com/JBavitha/pes_sdw/assets/142578450/f62f23de-03bb-40b7-94f1-8561c057ec22)

## GLS(Gate Level Simulation)

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v pes_sdw_net.v tb_pes_sdw.v
```

![image](https://github.com/JBavitha/pes_sdw/assets/142578450/bbc59e49-52b6-4853-86c3-e5f6ffab2ad5)


```
./a.out
gtkwave pes_sdw_tb.vcd 
```
![Screenshot from 2023-10-21 12-10-08](https://github.com/JBavitha/pes_sdw/assets/142578450/c628d6b0-404a-4a61-8efb-23a7a9847545)
# Physical design 

- Physical design is the essential procedure that converts an abstract depiction of an electronic system, like an integrated circuit or computer chip, into a practical layout fit for manufacturing. This intricate process involves a series of stages for organizing and structuring different components, such as transistors, wiring, and connections, on a semiconductor material.

Key facets of physical design encompass:

 - Floorplanning: Defining the spatial arrangement of components and modules within the chip's layout.
 - Placement: Positioning individual elements like transistors and logic gates efficiently on the semiconductor substrate.
 - Routing: Establishing the interconnections or wiring between these components to facilitate data flow.
 - Clock Tree Synthesis (CTS): Structuring the clock distribution network to ensure precise synchronization throughout the chip.
 - Power Planning: Managing power distribution and consumption to maintain optimal operation and minimize energy usage.
 - Signal Integrity Analysis: Assessing the integrity of signals during transmission to prevent interference or distortion.
 - Timing Analysis: Evaluating the timing of signal propagation to meet performance requirements and minimize delays.
 - Design for Testability (DFT): Incorporating features that simplify testing and fault detection during chip production.
 - Physical Verification: Conducting rigorous checks to confirm that the physical design adheres to design rules and is free from errors.
 - Package Design: Creating the external packaging of the chip, considering factors like heat dissipation and connectivity.

# Installation
### ngspice
- Download the tarball from `https://sourceforge.net/projects/ngspice/files/` to a local directory
- 
```
cd $HOME
sudo apt-get install libxaw7-dev
tar -zxvf ngspice-41.tar.gz
cd ngspice-41
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
sudo make
sudo make install
```















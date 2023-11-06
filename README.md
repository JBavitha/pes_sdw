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

<details>

<summary>RTL Synthesis and GLS Simulation</summary>



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

</details>

<details>

<summary>Physical Design</summary>



# Physical design 

- Physical design is the essential procedure that converts an abstract depiction of an electronic system, like an integrated circuit or computer chip, into a practical layout fit for manufacturing. This intricate process involves a series of stages for organizing and structuring different components, such as transistors, wiring, and connections, on a semiconductor material.

**Key facts of physical design encompass:**

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

## Installation of tools:

**Openlane and Docker**

- Follow the steps in the below link to install Docker
  https://docs.docker.com/engine/install/ubuntu/

- To install Openlane2
  https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html

### Magic

- Follow the below steps to install magic

```
git clone https://github.com/RTimothyEdwards/magic  
$ sudo apt-get install m4  
$ sudo apt-get install tcl-dev  
$ sudo apt-get install tk-dev  
$ sudo apt-get install blt  
$ sudo apt-get install freeglut3  
$ sudo apt-get install libglut3  
$ sudo apt-get install libglu1-mesa-dev  
$ sudo apt-get install libgl1-mesa-dev  
$ sudo apt-get install csh  
$ ./configure  
$ make  
$ make install
```

### Step 1
- To begin the physical design process, we must create the design file for the "pes_sdw" project. This entails having the "pes_sdw.v" file and access to the Skywater Process Design Kit (PDK), which contains all the necessary foundry-provided PDK-related files. To accomplish this, we follow these steps within the Openlane design directory:
- Create a folder called "pes_sdw" within the design directory.
- Within the "pes_sdw" folder, establish two subfolders named "src" and "config.json".
- To make the config.json file we type the following: vim config.json

```config.json``` looks like 


![image](https://github.com/JBavitha/pes_sdw/assets/142578450/1a2e13a0-54ad-492a-82c4-231dd925c983)


- after this, we go to the src file and add the pes_sdw.v file that we generated from Yosys in RTL synthesis and the required PDKs for our design.

### Step 2

- we invoke the openlane.

```
cd OpenLane
make mount
./flow.tcl -interactive
package require openlane 0.9
prep -design pes_sdw
```


<img width="604" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/0ea08725-c509-46b0-84e5-a2d1688ee621">


![image](https://github.com/JBavitha/pes_sdw/assets/142578450/93ba2e58-633e-42be-a5a0-7179152fad58)


```run_synthesis```

<img width="610" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/3307d948-871f-4412-97fb-69cbfdaf4c94">

- We can find the following synthesis report file in

```Openlane/designs/pes_sdw/runs/<latest_run>/reports/synthesis```

<img width="448" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/a1dab21c-b818-47c2-bb17-1375a0f0925a">


## FLOORPLAN

```run_floorplan```


- To locate pes_sdw.def file for floorplan we type following command
```
cd OpenLane/designs/pes_sdw/runs/RUN_2023.11.03_05.32.49/results/floorplan
ls
```
![Screenshot from 2023-11-03 18-28-49](https://github.com/JBavitha/pes_sdw/assets/142578450/2a670b2c-ca32-49e0-a187-acaf155d3225)


- now to view the floorplan we type the following command:

```
cd OpenLane/designs/pes_sdw/runs/RUN_2023.11.03_05.32.49/results/floorplan
magic -T /home/bavitha/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_sdw.def &
```

<img width="475" alt="Screenshot 2023-11-03 134156" src="https://github.com/JBavitha/pes_sdw/assets/142578450/778adc35-786c-489a-9b79-41a6904029a7">


<img width="471" alt="Screenshot 2023-11-03 134233" src="https://github.com/JBavitha/pes_sdw/assets/142578450/831c37b2-91e3-4d91-a219-ea9e220ece7a">


<img width="484" alt="Screenshot 2023-11-03 134317" src="https://github.com/JBavitha/pes_sdw/assets/142578450/f4f8f81a-1e93-4504-8602-8c3ee4f356cd">


## PLACEMENT:

```run_placement```

- Follow the below steps
```
cd OpenLane/designs/pes_sdw/runs/RUN_2023.11.03_05.32.49/results/placement
magic -T /home/bavitha/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_sdw.def &

```

<img width="476" alt="Screenshot 2023-11-03 134801" src="https://github.com/JBavitha/pes_sdw/assets/142578450/17ea5c8d-6b31-46a5-9796-61df13790e15">


<img width="476" alt="Screenshot 2023-11-03 134826" src="https://github.com/JBavitha/pes_sdw/assets/142578450/7d89503b-b1bd-4d53-a171-918c559db244">


**placement statistics**


```Openlane/designs/pes_sdw/runs/<latest run>/logs/placement```


<img width="450" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/757243ff-8bc0-4652-9267-2840671a1ed7">


### ROUTING:

```run_routing```

- follow below steps
```
cd OpenLane/designs/pes_sdw/runs/RUN_2023.11.03_05.32.49/results/routing
magic -T /home/bavitha/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_sdw.def &

```


<img width="478" alt="Screenshot 2023-11-03 135031" src="https://github.com/JBavitha/pes_sdw/assets/142578450/1050fd08-d552-470a-b8f1-d1bb1e3ac5b0">


<img width="478" alt="Screenshot 2023-11-03 135109" src="https://github.com/JBavitha/pes_sdw/assets/142578450/5c10d76c-7ad3-462f-a89a-94ceee616820">


<img width="485" alt="Screenshot 2023-11-03 135147" src="https://github.com/JBavitha/pes_sdw/assets/142578450/30e4eaef-b67d-4675-ba6e-c17650e4b3f0">


**Routing analysis**

```Openlane/designs/pes_bc/runs/<latest run>/logs/routing```

<img width="449" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/9ae64a25-12d1-4147-a0c9-32fe6fc1ac76">


<img width="449" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/99a07c73-bd51-42c7-bfdf-3da7f2149fbe">


### Clock tree synthesis

```run_cts```

<img width="602" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/8b8dde79-3fd2-477c-a801-00f7bf3cab0e">

**cts statistics**

<img width="450" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/74e36b43-e73f-4e15-a149-827272a430d3">


### Automatic flow in Openlane:

```
make mount

./flow.tcl -design <design name>

```

<img width="599" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/90213bc0-2d5d-442e-890e-4e2b15d1ada1">

- Flow completion

<img width="558" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/7c65e615-3a95-4cdc-b4cb-9be56474be7d">


### PARAMETERS

**Post-layout Synthesis**



<img width="448" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/a1dab21c-b818-47c2-bb17-1375a0f0925a">

Gate count = 


**Area**

<img width="489" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/b9e75b59-a9bb-489a-ae29-f8c9be07b093">







**Summary report**

<img width="558" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/b1d20fbc-4420-4b5c-9a40-1012363fd5d3">




**4.Power**

<img width="450" alt="image" src="https://github.com/JBavitha/pes_sdw/assets/142578450/74e36b43-e73f-4e15-a149-827272a430d3">









</details>





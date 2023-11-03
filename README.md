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
### magic
```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
sudo make
sudo make install
```
### Openlane
```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 
# After reboot
docker run hello-world (should show you the output under 'Example Output' in https://hub.docker.com/_/hello-world)

- To install the PDKs and Tools
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

### Step 1
- To begin the physical design process, we must create the design file for the "pes_sdw" project. This entails having the "pes_sdw.v" file and access to the Skywater Process Design Kit (PDK), which contains all the necessary foundry-provided PDK-related files. To accomplish this, we follow these steps within the Openlane design directory:
Create a folder called "pes_sdw" within the design directory.
Within the "pes_sdw" folder, establish two subfolders named "src" and "config.tcl."
To make the config.tcl file we type the following: vim config.tcl

```
set ::env(DESIGN_NAME) "pes_sdw"

set ::env(VERILOG_FILES) "./designs/pes_sdw/src/pes_sdw.v"

set ::env(CLOCK_PERIOD) "10.000"
set ::env(CLOCK_PORT) "clk"
set ::env(CLOCK_NET) $::env(CLOCK_PORT)

set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1} {
        source $filename
}
```
```config.json``` looks like 
![image](https://github.com/JBavitha/pes_sdw/assets/142578450/1a2e13a0-54ad-492a-82c4-231dd925c983)


- after this, we go to the src file and add the pes_sdw.v file that we generated from Yosys in RTL synthesis and the required PDKs for our design.
### Step 2
- we invoke the openlane.
```
cd OpenLane
make mount
./flow.tcl -design <DESIGN NAME>

```
![image](https://github.com/JBavitha/pes_sdw/assets/142578450/93ba2e58-633e-42be-a5a0-7179152fad58)


## FLOORPLAN

- To locate pes_sdw.def file for floorplan we type following command
```
cd OpenLane/designs/pes_sdw/runs/RUN_2023.11.03_05.32.49/results/floorplan
ls
```
![Screenshot from 2023-11-03 18-28-49](https://github.com/JBavitha/pes_sdw/assets/142578450/2a670b2c-ca32-49e0-a187-acaf155d3225)


- now to view the floorplan we type the following command:

```
magic -T /home/bavitha/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_sdw.def &
```
<img width="475" alt="Screenshot 2023-11-03 134156" src="https://github.com/JBavitha/pes_sdw/assets/142578450/778adc35-786c-489a-9b79-41a6904029a7">

<img width="471" alt="Screenshot 2023-11-03 134233" src="https://github.com/JBavitha/pes_sdw/assets/142578450/831c37b2-91e3-4d91-a219-ea9e220ece7a">

<img width="484" alt="Screenshot 2023-11-03 134317" src="https://github.com/JBavitha/pes_sdw/assets/142578450/f4f8f81a-1e93-4504-8602-8c3ee4f356cd">

## PLACEMENT:
- First change the directory to
```
cd OpenLane/designs/pes_sdw/runs/RUN_2023.11.03_05.32.49/results/placement
magic -T /home/bavitha/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read
magic -T /home/bavitha/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_sdw.def &

```

<img width="476" alt="Screenshot 2023-11-03 134801" src="https://github.com/JBavitha/pes_sdw/assets/142578450/17ea5c8d-6b31-46a5-9796-61df13790e15">

<img width="476" alt="Screenshot 2023-11-03 134826" src="https://github.com/JBavitha/pes_sdw/assets/142578450/7d89503b-b1bd-4d53-a171-918c559db244">

### ROUTING:

<img width="478" alt="Screenshot 2023-11-03 135031" src="https://github.com/JBavitha/pes_sdw/assets/142578450/1050fd08-d552-470a-b8f1-d1bb1e3ac5b0">

<img width="478" alt="Screenshot 2023-11-03 135109" src="https://github.com/JBavitha/pes_sdw/assets/142578450/5c10d76c-7ad3-462f-a89a-94ceee616820">

<img width="485" alt="Screenshot 2023-11-03 135147" src="https://github.com/JBavitha/pes_sdw/assets/142578450/30e4eaef-b67d-4675-ba6e-c17650e4b3f0">


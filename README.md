# HAPS FPGA Design and Verification Example

---
### Course Aim
* Hardware features
    * FPGA reference design for PS+PL on HAPS system architecture architecture
    * AXI-C2C interface between PS (Cortex-A53) and PL on HAPS
    * DDR controller and 16GB DRAM on HAPS
    * Microbloaze MCU with virtual UART port for simulation and emulation 
* Software features
    * Vitis software flow for building Microblaze baremetal software
    * Embedded software reference for running on Microblaze MCU
    * Running MCU software on both simuation abd FPGA emulation 

---
### Course Prerequisites
* Verilog design and simluation 
* FPGA design and implementaiton methodology
* AMBA-based SoC architecture and peripherals
* Embedded software programming

---
### Syllabus

| # | Training Module | Page | Description |
|:-:|:-|:-|:-|
| 1 | Vivado HW Development Flow | [Page](https://github.com/heslabs/haps_mcu_v22p2/tree/main/01_Create_HW_Design) | Create RTL hardware design using Vivado |
| 2 | Vitis SW Development Flow | [Page](https://github.com/heslabs/haps_mcu_v22p2/tree/main/02_Create_Application_SW) | Build MCU baremetal software using Vitis |
| 3 | Vivado Simulation Flow | [Page](https://github.com/heslabs/haps_mcu_v22p2/tree/main/03_Run_RTL_Simulation) | Running Verilog simulation using Vivado |
| 4 | Running RTL Simulation with Software | [Page](https://github.com/heslabs/haps_mcu_v22p2/tree/main/04_Run_Software_Application) | Running application software in RTL simulation |
| 5 | Configure and Program FPGA | [Page](https://github.com/heslabs/haps_mcu_v22p2/tree/main/05_Program_FPGA) | Configure HAPS and Program FPGA using Confpro-SX GUI |
| 6 | Running FPGA Emulation with Software | [Page](https://github.com/heslabs/haps_mcu_v22p2/tree/main/06_Run_FPGA_Emulation) | Running application software in FPGA emulation |

---
### FPGA Lab Tools

* 2024.2
   * AMD Unified Installer for FPGAs & Adaptive SoCs (2024.2) [[docs]](https://docs.amd.com/r/en-US/ug973-vivado-release-notes-install-license/Download-and-Installation)
   * Installing the Vitis Software Platform (2024.2) [[docs]](https://docs.amd.com/r/en-US/ug1400-vitis-embedded/Installing-the-Vitis-Software-Platform)
 
---
### Setup global environment variables

| FPGA Tools | Vendor | Settings |
|:-|:-|:-|
| HAPS-SX Configuration Tools | E=Elements | /home/eda/Confpro-SX/guibin/Confpro-SX-GuiRun.sh  |
| Vitis&Vivado License | AMD-Xilinx |export XILINXD_LICENSE_FILE=~/.Xilinx/Xil_License.lic | 
| AMD-Xilinx Vivado | AMD-Xilinx |export VIVADO_HOME=/home/Vivado/Vitis/2024.2 | 
| AMD-Xilinx Vitis | AMD-Xilinx |export VITIS_HOME=/home/eda/Vitis/2024.2 |  
| AMD-Xilinx Vitis HLS | AMD-Xilinx |export VITIS_HLS_HOME=/home/eda/Vitis_HLS/2024.2 |  

---
### FPGA Prototyping Platform - Lab setup
**Compile Your Vivado Design in Local and Emulate your Design in the Cloud**

<img src="https://github.com/user-attachments/assets/713f953a-b265-42f8-8df8-45b70c512401" width=850>

---

| Device | IP Address | Description | Smart WiFi Plug |
|:-|:-|:-|:-|
| HAPS-VU19P | 192.168.50.2 | HAPS-SX VU19P | 192.168.50.92 |
| HAPS-ZYNQ | 192.168.50.3 | HAPS SMF ZynqMPSoC/CA53 module | 192.168.50.93 |
| HAPS-PC | 192.168.50.5 | Linux PC | 192.168.50.95 |


* The smart WiFi plug is used to reset HAPS-ZYNQ after HAPS-FPGA programmed
   * Tapo P105 | Mini Smart Wi-Fi Plug [[Tapo]](https://www.tapo.com/en/product/smart-plug/tapo-p105/)

---
### Remote access to HAPS Hardware Platform

* EPS-VU19P
   * https://github.com/heslabs/haps19p_base_v24p2
* EPS-VU13P
   * https://github.com/heslabs/haps13p_base_v24p2

---
### HAPS-SX and Daughter card

<img src="https://github.com/user-attachments/assets/23fcf5dd-3bff-45a7-8453-76a189d734e6" width=850>



---
### FPGA Hardware and Software Design Flow
1. Create HDL Design using Vivado
   * Create Block Diagram Design using Vivado
   * Configure MicroBlaze Processor
   * Build Hardware Design
2. Create Application Software Using Vitis
   * Create Platform Project from the XSA
   * Create a new Application Project on Platform
   * Associate ELF and Generate Bitstream (Optional)
3. Connecting FPGA Hardware  
   * Connecting HAPS Hardware using Confpro
   * Connecting HAPS Hardware using Vivado
   * Connecting HAPS Hardware using XSCT
4. Launch Application Software 
   * Launch Application Software using Vitis
   * Launch Application Software using XSCT


<img src="https://github.com/user-attachments/assets/e6c5ff7d-928b-40f9-9ec6-9f090a308535" width=650>

---
### AMBA-based SoC Architecture

<img src="https://github.com/user-attachments/assets/c8baf5aa-a481-4689-8ffa-03971eac20e4" width=850>

---
### Leverage Cortex-A53 CPU subsystem in AMD-Xilinx ZynqMPSoC 
<img src="https://github.com/user-attachments/assets/285e3d75-bbee-47f5-a2d2-3137a261021c" width=850>

---  
### 1. Vivado HW Development Flow

* Create design based on prebuit reference (top.tcl) \
  ```$ make new```
* Add your custom IP into the referecne and validate it
* Export the hardware in Vivado (top_wrapper.xsa) \
  ```$ make exp```

---  
### 2. Vitis SW Development Flow

* Create new application project in Vitis \
  ```$ make app-new```
* Select the xsa file from hardware export for platform   
* Enter the platform name: "main", this will be used in tcl command later  
* Create C/C++ program from the template
* Modify the application C/C++ codes
* Build the Vitis project and geenrate the exectuable binary (main.elf)

--- 
### 3. Vivado Simulation Flow
* Association the elf files in Vivado
* Export the simulation for Vivado XSIM simualtor
* Lunch the generated testbench script "tb.sh"
* Open the dumped waveform file (*.wdb) with selected signals (tb_behav.wcfg)

---
### 4. Application SW Test Flow

* Copy the application source from workspace
  ```
  $ cd ./appsw/memorytests
  $ cp -rf ../workspace/main/src .
  ```
  
* Modify the application code in command mode \
  ```$ vim ./appsw/memorytests/src/memorytest.c```
  
* Build the Vitis project and generate elf file in command mode \
  ```$ make app-cmd```
  
* Launch the RTL simulaiton and view the dumped waveform \
  ```$ make sim```
  
* Copy the simulation waveform (*.wdb) into SW test case
  ```
  $ cd ./vivado && ln -s ../appsw/$(APP)/tb.wdb .
  $ cd ./vivado && cp -f ../appsw/$(APP)/tb_behav.wcfg .
  ```
  
* Launch waveform viewer for SW test case
  ```
  $ cd ./vivado && vivado -mode gui -project ./$(PRJ).xpr -source ../appsw/$(APP)/xsim_wave.tcl &
  ### xsim_wave.tcl
  set_property target_simulator XSim [current_project]
  open_wave_database {./tb.wdb}
  open_wave_config  -quiet ./tb_behav.wcfg
  ```

---
### 5. Config HAPS and Program FPGA

Launch Confpro-SX GUI tools
```
$ export CONFPRO_HOME=/home/eda/Confpro-SX_1.1.10
$(CONFPRO_HOME)/guibin/Confpro-SX-GuiRun.sh
/home/eda/Confpro-SX_1.1.10/guibin/Confpro-SX-GuiRun.sh (/bin/Confpro-SX)
```

---
### 6. Run FPGA Emulation Flow

* Download embedded software and launch emulation
* Download your application software for Microblaze MCU and launch the FPGA emulaiton at runtime. Note that the prerequisites are the FPGA bitstream was successfully programmed and the Microblaze MCU in the HW design works funcitonal.
* Prepare you application software "apps.elf"
* Launch Xilinx system command line tool with tcl script
* Check the results in "uart.log"


#### Launch console in GUI mode
```
xsct ./xsct_uartgui.tcl 192.168.50.2:2542 ./PASS.elf
```

#### Launch console in command mode
```
xsct ./xsct_uartcmd.tcl 192.168.50.2:2542 ./PASS.elf; cat ./uart.log
```


---
### Smart power Plug

* The smart WiFi plug is used to reset HAPS-ZYNQ after HAPS-FPGA programmed
   * Tapo P105 | Mini Smart Wi-Fi Plug [[Tapo]](https://www.tapo.com/en/product/smart-plug/tapo-p105/)
   * Tapo API Client for TP-Link Tapo smart devices: [[Github]](https://github.com/mihai-dinculescu/tapo)
     
<img src="https://github.com/user-attachments/assets/8188a214-84a8-4690-a463-b4a203c61510" width=120>
<img src="https://github.com/user-attachments/assets/f86ed397-0a8d-4069-b3f5-4957a68ec6c8" width=120>





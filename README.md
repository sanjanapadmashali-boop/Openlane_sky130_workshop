# Sky130 Digital VLSI SoC Design using OpenLANE
This repository documents my learning and hands-on work from the VSD IAT Digital VLSI SoC Design course. It covers five days of theory and practical labs, including a complete RTL-to-GDSII ASIC implementation using the OpenLANE flow with the SkyWater 130nm PDK, covering synthesis, floorplanning, placement, routing, STA, and GDS generation.



## Day 1 – Inception of Open-Source EDA, OpenLANE, and Sky130 PDK

## Software–to–Silicon Stack Overview

Modern digital systems are built as a layered stack, where each layer abstracts complexity from the one above it. Software never interacts directly with transistors — the **Instruction Set Architecture (ISA)** is the formal contract between software and hardware.

### 1. Application Software
User-level programs such as stopwatches, calculators, and browsers.
- Written in high-level languages (C, C++, Python, Java)
- Hardware-independent
- Relies on system software and compilers

### 2. System Software
Manages hardware resources and provides services to applications.
- Operating Systems (Linux, Windows)
- Device drivers, memory management, I/O handling
- Bridges application software and hardware

### 3. Compiler & Assembler
- Compiler translates high-level code (C/C++) into ISA-specific assembly
- Assembler converts assembly into binary machine code (ELF/executable)
- Same source code can run on different processors with the appropriate compiler

### 4. Instruction Set Architecture (ISA – RISC-V)
Defines **what** instructions a processor can execute, not **how** it is implemented.
- Open-source, modular, and extensible
- Widely used in industry and academia
- Acts as the legal interface between software and hardware

### 5. Microarchitecture (RTL)
Implements the ISA at the Register Transfer Level (RTL).
- Written in Verilog/VHDL
- Example core: PicoRV32
- Includes instruction decoding, registers, control logic, and datapath
- Multiple microarchitectures can implement the same ISA

### 6. Physical Design & Fabrication
- RTL is synthesized to gates, placed and routed
- Timing closure and physical verification
- Final chip is manufactured using foundry PDK rules

### Key Insight
**Software depends on the ISA, not on the hardware implementation.**  
As long as the ISA contract is honored, the same software can run on different CPUs.

### ASIC Design Flow (RTL to GDSII)
The complete ASIC design flow includes:
1. Specification
2. RTL Design (Verilog)
3. Functional Verification
4. Logic Synthesis
5. Floorplanning
6. Placement
7. Clock Tree Synthesis (CTS)
8. Routing
9. Sign-off Checks (DRC, LVS, STA)
10. GDSII Generation

### Open-Source EDA Tools
Open-source EDA tools make chip design accessible and affordable:
- **Yosys** – Logic synthesis
- **OpenLANE** – RTL-to-GDSII flow
- **Magic** – Layout and DRC
- **OpenSTA** – Static Timing Analysis
- **ngspice** – Circuit simulation

### Sky130 PDK
The **Sky130 Process Design Kit (PDK)** provides:
- Device models
- Design rules
- Standard cell libraries  
Released by **SkyWater Technology**, Sky130 is fully open-source.

#### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/4172b91fdf93b614cc12a4f91c14e612b136c931/flo_tcl_interactive.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1__cell_ratio.png)
#### 2.claculate flop ratio
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1_flop_ratio.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1_flop_ratio_dff.png)
% of dff = 10.84%

## Day 2 – Good Floorplan vs Bad Floorplan & Introduction to Library Cells

### Floorplanning
Floorplanning defines the physical layout of the chip, including:
- Die area
- Core area
- IO placement
- Power planning

### Die Area and Core Area
- **Die Area**: Total chip area
- **Core Area**: Area containing standard cells

### Aspect Ratio and Utilization
- Aspect Ratio = Height / Width
- Utilization = (Standard Cell Area / Core Area)

### Power Planning
A good power plan ensures reliable operation using:
- VDD rails
- VSS (ground) rails
- Power rings and straps

### Good vs Bad Floorplan
**Good Floorplan**
- Balanced utilization
- Minimal congestion
- Improved timing

**Bad Floorplan**
- Routing congestion
- IR drop issues
- Timing violations

### Standard Cell Libraries
Standard cell libraries contain:
- **Combinational cells**: AND, OR, MUX
- **Sequential cells**: Flip-flops, Latches
run_floorplan
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_2_run_floorplan.png)
opening_floorplan_def file
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/opening_floorplan_def_file.png)

-1 unit distance = 1 micron 
-die width = 660.685 microns
-die height = 671.405 microns
-area of die = 660.685*671.405=443587.2 sq microns
#### 3. Load generated floorplan def in magic tool and explore the floorplan.
floorplan def in magic
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/floorplan_def_in_magic.png)

Equdistant placement of ports
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/b275acad76417a4ff64f5f857edaea94b294c31a/equidisstance_plaement_ports.png)
#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
run placement
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/b275acad76417a4ff64f5f857edaea94b294c31a/run_placement.png)

#### 5. Load generated placement def in magic tool and explore the placement.
floorplan.def in magic 
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/b275acad76417a4ff64f5f857edaea94b294c31a/floorplan_def_in_magic2_placement.png)


### Key Learnings
- Impact of floorplan on performance and area
- Core utilization and aspect ratio
- Basics of standard cell design and placement

## Day 3 – Design Library Cell using Magic Layout and Ngspice Characterization
### CMOS Inverter
The CMOS inverter is the basic building block of digital circuits and is used to understand:
- Transistor sizing
- Layout techniques
- Performance metrics

### Layout using Magic
Magic is used to:
- Create layout geometries
- Perform DRC checks
- Extract netlists

### Design Rules
Design rules ensure manufacturability:
- Minimum width
- Minimum spacing
- Enclosure rules

### SPICE Characterization
Using **ngspice**, the following parameters are measured:
- Propagation delay
- Rise time
- Fall time
- Power consumption

#### 1. Clone custom inverter standard cell design from github
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/b275acad76417a4ff64f5f857edaea94b294c31a/clone_custom_inv_commands.png)
#### 2. Load the custom inverter layout in magic and explore.
nmos and pmos identified
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/b275acad76417a4ff64f5f857edaea94b294c31a/nmos_pmos_identified.png)
#### 3. Spice extraction of inverter in magic.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/d0402995ea9edc95d036a46b38c978786d4d0654/tkcon_window_spice_commands.png)
screenshot of file created
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/d0402995ea9edc95d036a46b38c978786d4d0654/spice_file_created.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/d0402995ea9edc95d036a46b38c978786d4d0654/ngspice_run.png)
### 4.Editing the spice model file for analysis through simulation.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/745011b75a795b7aaaabbc60e3e74d5205e21c7f/edited_spice_file.png)
grid command
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/7813d2055e1e4a6a21ad43d74bf45aca57c9e443/grid_command_run.png)
### 5.Post-layout ngspice simulations
commands for ng spice simulation
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/generated_plot_after_changes.png)
generated plot
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/delay_calc_20_80_perc_outputs.png)
-o/p of 20% at 0.66v is 2.122
-o/p of 80% at 2.64v is 2.249 
-fall trasition time  = 2.249-2.122 = 0.127 ns
generated plot
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/rise_delay_fall_delay_calc.png)
rise cell delay = 2.214-2.149 = 0.065ns
### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.
Screenshot of commands run
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commans_run_drc_tests.png)
Screenshot of .magicrc file 
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sc_of_magicrc.png)
#### Screenshot incorrectly implemented poly.9 , no drc voilation even though spacing is <0.48
![images alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/implementation_of_poly.9_drc_voilation.png)
drc voilation
![images alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/drc_voilation.png)
rules
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/diff_rules.png)
commands inseted in sky130A.tech file
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_inserted_insky130_techfile.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_inserted_insky130_techfile2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_inserted_insky130_techfile3.png)

![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/dnwell2.jpeg)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/dnwell1%20(2).jpeg)

### Key Learnings
- CMOS inverter layout design
-  Custom standard cell design using Magic
- DRC and LVS checks
- Circuit extraction and simulation using ngspice

## Sky130 Day 4 – Pre-layout Timing Analysis and Importance of Good Clock Tree

### Overview
- Static Timing Analysis (STA) fundamentals
- Pre-layout timing analysis
- Clock tree design concepts
- ### Timing Concepts

Timing analysis ensures that data is transferred correctly between sequential elements within the required clock period. The key timing parameters are:

- **Setup Time**  
  The minimum amount of time that data must be stable **before the active clock edge** so that it can be reliably captured by a flip-flop.  
  Violation of setup time leads to **setup timing failures**, usually caused by slow data paths.

- **Hold Time**  
  The minimum amount of time that data must remain stable **after the active clock edge**.  
  Hold violations occur when data paths are too fast and change too quickly after the clock edge.

- **Clock-to-Q Delay (Tcq)**  
  The delay between the active clock edge and the change in output (Q) of a flip-flop.  
  This delay directly affects the timing of the next logic stage.

- **Slack**  
  Slack is the difference between **required time** and **actual arrival time** of a signal.  
  - Positive slack → Timing met  
  - Negative slack → Timing violation  

---

### Pre-Layout Timing Analysis

Pre-layout timing analysis is performed **before physical design** using estimated wire delays.  
It helps designers:

- Identify **critical paths** early
- Evaluate design performance at the RTL or gate level
- Fix timing issues before placement and routing
- Reduce the risk of major timing failures during sign-off

Although interconnect delays are estimated, pre-layout analysis provides a **baseline for timing closure**.

---

### Clock Tree Synthesis (CTS)

Clock Tree Synthesis is the process of building a **balanced clock distribution network** that delivers the clock signal to all sequential elements simultaneously.

CTS involves:
- Inserting clock buffers and inverters
- Balancing clock path lengths
- Minimizing clock skew and latency

A well-designed clock tree is essential for achieving reliable and high-speed operation in synchronous circuits.

---

### Clock Skew and Latency

- **Clock Skew**  
  Clock skew is the difference in clock arrival time between two sequential elements.  
  Excessive skew can cause:
  - Setup violations
  - Hold violations
  - Unpredictable circuit behavior

- **Clock Latency**  
  Clock latency is the total time taken by the clock signal to propagate from the clock source to a register.  
  Latency affects the overall performance and must be controlled during CTS.

---

### Importance of Clock Tree Synthesis

Clock Tree Synthesis plays a crucial role in physical design by:

- Minimizing clock skew across the design
- Reducing setup and hold timing violations
- Improving timing closure
- Ensuring reliable synchronous operation
- Enhancing overall chip performance and stability

### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
Conditions to be verified before moving forward with custom designed cell layout:

Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
Condition 3: Height of the standard cell should be even multiples of the vertical track pitch
screenshot of tracks.info of sky_fd_hd
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/tracks_info_sky130_fd_sc_hc.png)
grid
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/grid_command_run.png)
conditions verfied
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/conditions_verified.png)
newly created_lef_file
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/created_lef_file.png)
copying files to picorv32a
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/copying_files_commands.png)
edit config.tcl
Run openlane flow synthesis with newly inserted custom inverter cell.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/run_synth_commands.png)
Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/after_synthesis.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/area_rreduced_.png)
Commands to view and change parameters to improve timing and run synthesis
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commans_to_change_parameters.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_floorplan.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/command_to_clear_errors_in_fp.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/command_to_clear_errors_in_fp2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/run_placement2.png)
Screenshot of merged.lef in tmp directory with our custom inverter as macro
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/merged.lef_file.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/synthesis_sucessfull.png)
using tag -overwrite
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/using_tag.png)
after parameters changed synthesis sucessfull and slack became 0
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/synthesis_sucessfull_after_parameters.png)
placement def in magic
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/placement_def_in_magic.png)
internal layers of cells
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/internal_layers_of_cells.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/run_synthesis_final.png)
slack voilated
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sta_slack_voilated.png)
fanout commands
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/fanout_commands.png)
slack report
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/slack_r.png)
created my_base_sdc folder
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/my_base_sdc.png)
sta reports
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sta_run_1.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sta_run_2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sta_run_3.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sta_run_4.png)
or gate of strength 2 driving 4 fanouts
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/or_gate_2str_driving_4_fanouts.png)
commands to optimize timing of or to strength 4
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_optimize_timing_or_to_str_4.png)
sta reports
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/report_sta_1.png)
sta or gate strength 2 drivung oa gate
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sta_or_gate_str2_driving_oa_gate.png)
slack reduced
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/slack_reduced_1.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/reduced_slack2.png)
Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_to_make_cp_of_netlist.png)
commands to wwrite verilog
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_write_verilog.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/verified_netlist_or_4_4.png)
Commands load the design and run necessary stages
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_run_synthesis.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/synthesis_sucessfull_after_write_verilog.png)
floorplan 
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/run_floorplan_after_write_verilog.png)
placement 
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/placement_done.png)
run_cts
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/placement_done_run_cts.png)
cts_done
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/cts_done.png)
Post-CTS OpenROAD timing analysis.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/post_cts.png)
Screenshots of commands run and timing report generated
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/post_cts_openroad_commands.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_openlane2.png)

![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/report_checks1.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/report_checks2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/report_checks3.png)
 post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/post_cts_ta_removing_clk_buff.png)
screenshots of commands and timing reports generated
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_timing_report1.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_timing_report2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_timing_report3.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_timing_report4.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_timing_report5.png)

### Key Learnings
- Setup and hold timing constraints
- Clock skew and jitter
- Importance of balanced clock distribution

## Day 5 – Final Steps for RTL-to-GDS using TritonRoute and OpenSTA

Day 5 focuses on completing the **physical design flow** and performing **final sign-off checks** to ensure the design is ready for fabrication. This stage converts the placed and clocked design into a manufacturable layout.

---

### Routing

Routing is the process of creating physical interconnections between all placed standard cells while satisfying design rules and timing constraints.

Routing is performed in two stages:

- **Global Routing**  
  Global routing determines the high-level routing paths between cells by dividing the design into routing regions.  
  It focuses on:
  - Estimating routing resources
  - Avoiding congestion
  - Providing routing guides for detailed routing  

- **Detailed Routing**  
  Detailed routing performs exact wire placement based on global routing guides.  
  It ensures:
  - Precise metal layer assignment
  - Proper via insertion
  - Compliance with all design rules  

In OpenLANE, **TritonRoute** is used for detailed routing, producing a **DRC-clean layout**.

---

### Sign-off Checks

Sign-off checks validate that the design meets **manufacturing, logical, and timing requirements**.

- **DRC (Design Rule Check)**  
  Verifies that the layout follows all fabrication rules defined by the Sky130 PDK, such as:
  - Minimum spacing
  - Minimum width
  - Enclosure rules  
  DRC-clean layout is mandatory before fabrication.

- **LVS (Layout vs Schematic)**  
  Ensures that the physical layout matches the synthesized netlist.  
  LVS checks:
  - Correct connectivity
  - Proper device instantiation
  - No missing or extra components  

- **STA (Static Timing Analysis)**  
  Static Timing Analysis verifies that all timing paths meet setup and hold constraints without requiring simulation.  
  **OpenSTA** is used to:
  - Analyze critical paths
  - Verify clock constraints
  - Confirm timing closure  

---




cts_done_gen pdn
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/cts_done_gen_pdn.png)
pdn in magic
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/PDN_def_in_magic.png)
commands to load pdn
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_to_load_pdn.png)
zero violations
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/zero_voilations.png)
routing done
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/routing_done.png)

![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/routing_done2.png)
routed def
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/routed_def.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/routed_def_2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/routed_def_3png.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/fast_route_guide.png)
Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/post_route_opensta_commands.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/post_routing_opensta_timing_report1.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/post_routing_opensta_timing_report2.png)


### Final Output

After successful routing and sign-off checks, the final outputs are generated:

- **GDSII File**  
  The final layout database containing all geometric information required for fabrication.

- **Fabrication-Ready Design**  
  A fully verified design that meets:
  - Functional correctness
  - Timing constraints
  - Manufacturing rules  

This marks the completion of the **RTL-to-GDSII flow**.
## Conclusion
This repository captures the complete RTL-to-GDSII flow and provides hands-on exposure to modern open-source VLSI design tools, reinforcing both theoretical understanding and practical ASIC implementation skills.
## Acknowledgements
**Kunal Ghosh**, Co-founder, VSD Corp. Pvt. Ltd.
**Nickson P Jose**, Physical Design Engineer, Intel Corporation.
**R. Timothy Edwards**, Senior Vice President of Analog and Design, efabless Corporation.

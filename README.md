# Openlane_sky130_workshop
This repository documents my learning and hands-on work from the VSD IAT Digital VLSI SoC Design course. It covers five days of theory and practical labs, including a complete RTL-to-GDSII ASIC implementation using the OpenLANE flow with the SkyWater 130nm PDK, covering synthesis, floorplanning, placement, routing, STA, and GDS generation.
# Sky130 Digital VLSI SoC Design using OpenLANE

### Sky130 Day 1 – Inception of Open-Source EDA, OpenLANE and Sky130 PDK

### Overview
- Introduction to open-source EDA ecosystem
- Understanding ASIC design flow
- Overview of OpenLANE architecture   [RTL Synthesis (Yosys),Static Timing Analysis (OpenSTA),DFT checks,Floorplanning,Placement,Clock Tree Synthesis (CTS),Routing (TritonRoute),RC Extraction,Physical Verification (DRC/LVS),GDSII generation]
-(OpenLANE is an **automated RTL‑to‑GDSII flow** for digital ASICs)
- Introduction to SkyWater 130nm PDK
#### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/4172b91fdf93b614cc12a4f91c14e612b136c931/flo_tcl_interactive.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1__cell_ratio.png)
#### 2.claclulate flop ratio
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1_flop_ratio.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1_flop_ratio_dff.png)
% of dff = 10.84%

## Sky130 Day 2 – Good Floorplan vs Bad Floorplan and Introduction to Library Cells
run_floorplan
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_2_run_floorplan.png)
opening_floorplan_def file
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/opening_floorplan_def_file.png)

1 unit distance = 1 micron 
die width = 660.685 microns
die height = 671.405 microns
area of die = 660.685*671.405=443587.2 sq microns
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

## Sky130 Day 3 – Design Library Cell using Magic Layout and Ngspice Characterization
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
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/generated_plot_after_changes.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/delay_calc_20_80_perc_outputs.png)
-o/p of 20% at 0.66v is 2.122
-o/p of 80% at 2.64v is 2.249 
-fall trasition time  = 2.249-2.122 = 0.127 ns


![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/rise_delay_fall_delay_calc.png)
rise cell delay = 2.214-2.149 = 0.065ns
### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.
Screenshot of commands run
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commans_run_drc_tests.png)
Screenshot of magicrc
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/sc_of_magicrc.png)
Screenshot incorrectly implemented poly.9 , no drc voilation even though spacing is <0.48
![images alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/implementation_of_poly.9_drc_voilation.png)
![images alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/drc_voilation.png)
rules
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/diff_rules.png)
commands inseted in sky130A.tech file
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_inserted_insky130_techfile.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_inserted_insky130_techfile2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_inserted_insky130_techfile3.png)


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
### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/tracks_info_sky130_fd_sc_hc.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/grid_command_run.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/conditions_verified.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/conditions_verified.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/tracks_info_sky130_fd_sc_hc.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/created_lef_file.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/copying_files_commands.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/run_synth_commands.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/after_synthesis.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/area_rreduced_.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commans_to_change_parameters.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/commands_floorplan.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/command_to_clear_errors_in_fp.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/command_to_clear_errors_in_fp2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/run_placement2.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/merged.lef_file.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/synthesis_sucessfull.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/using_tag.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/main/synthesis_sucessfull_after_parameters.png)












### Key Learnings
- Setup and hold timing constraints
- Clock skew and jitter
- Importance of balanced clock distribution

---

## Sky130 Day 5 – Final Steps for RTL to GDSII using TritonRoute and OpenSTA

### Overview
- Detailed routing using TritonRoute
- Design Rule Check (DRC)
- Post-route timing analysis using OpenSTA

### Key Learnings
- Routing completion and verification
- Parasitic extraction
- Post-layout timing closure
- Final GDSII generation

---

## Tools Used
- OpenLANE
- OpenROAD
- Magic VLSI
- Ngspice
- OpenSTA
- SkyWater 130nm PDK

---

## Conclusion
This repository captures the complete RTL-to-GDSII flow and provides hands-on exposure to modern open-source VLSI design tools, reinforcing both theoretical understanding and practical ASIC implementation skills.

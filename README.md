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
### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/4172b91fdf93b614cc12a4f91c14e612b136c931/flo_tcl_interactive.png)
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/task_1__cell_ratio.png)
### 2.claclulate flop ratio
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

floorplan def in magic
![image alt](https://github.com/sanjanapadmashali-boop/Openlane_sky130_workshop/blob/c042a06d230432430ded3c61686dfdb7f1079357/floorplan_def_in_magic.png)



### Key Learnings
- Impact of floorplan on performance and area
- Core utilization and aspect ratio
- Basics of standard cell design and placement

## Sky130 Day 3 – Design Library Cell using Magic Layout and Ngspice Characterization

### Overview
- Custom standard cell design using Magic
- DRC and LVS checks
- Circuit extraction and simulation using ngspice

### Key Learnings
- CMOS inverter layout design
- Parasitic extraction
- Timing and power characterization of cells

---

## Sky130 Day 4 – Pre-layout Timing Analysis and Importance of Good Clock Tree

### Overview
- Static Timing Analysis (STA) fundamentals
- Pre-layout timing analysis
- Clock tree design concepts

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

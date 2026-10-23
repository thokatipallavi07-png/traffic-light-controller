# traffic-light-controller
Traffic Light Controller Using Verilog HDL — RTL to GDSII

Project Description

The Traffic Light Controller is a digital VLSI project designed using Verilog Hardware Description Language (HDL). The main objective of this project is to control traffic signals at a road intersection using a Finite State Machine (FSM). The controller generates red, yellow, and green signals in a predefined sequence based on clock and reset inputs. The project follows the RTL-to-GDSII design flow, beginning with RTL coding and functional simulation, followed by logic synthesis and ASIC physical design. Functional verification is performed using Icarus Verilog, and simulation waveforms are analyzed using GTKWave. Logic synthesis is performed using Yosys, while OpenLane/OpenROAD and the Sky130 PDK can be used for physical-design stages such as floorplanning, power distribution network (PDN) generation, standard-cell placement, clock-tree synthesis (CTS), routing, static timing analysis (STA), physical verification, and GDSII generation, subject to the installed tools and configuration. This project provides practical experience in digital design, verification, synthesis, timing analysis, and ASIC implementation. Future improvements may include pedestrian crossing control, emergency-vehicle priority, and adaptive traffic signal timing.

Objectives

- Design a traffic light controller using Verilog HDL.
- Verify the design through testbench simulation and waveform analysis.
- Perform logic synthesis and analyze standard-cell utilization.
- Explore the complete ASIC physical-design flow from floorplanning to routing.
- Analyze timing reports and generate a final GDSII layout when supported by the configured flow.

Tools and Technologies

Verilog HDL, Icarus Verilog, GTKWave, Yosys, OpenLane/OpenROAD, Sky130 PDK, Ubuntu Linux, and Oracle VirtualBox.

Project Files

- "traffic_light.v" — Verilog RTL design.
- "traffic_light_tb.v" — Testbench for functional verification.
- "README.md" — Project documentation.
- "images/" — Simulation and physical-design screenshots.
- "reports/" — Synthesis and timing reports.
- "gds/" — Final GDSII layout, if generated.

Expected Outcomes

The project aims to demonstrate correct traffic-signal sequencing, successful RTL simulation, synthesis results, and the stages of ASIC physical design. Actual results, screenshots, timing reports, and layout files will be added after the corresponding stages have been completed and verified.

Traffic Light Controller Using Verilog HDL — RTL to GDSII

1. Project Description

The Traffic Light Controller is a digital VLSI project implemented using Verilog Hardware Description Language (HDL). It controls red, yellow, and green traffic signals in a predefined sequence using a Finite State Machine (FSM). The project demonstrates the RTL-to-GDSII design flow, including RTL design, functional simulation, logic synthesis, floorplanning, power distribution network (PDN) generation, placement, clock-tree synthesis (CTS), routing, static timing analysis (STA), and GDSII generation using a compatible OpenLane/OpenROAD flow and Sky130 PDK.

2. Objectives

- Design a traffic light controller using Verilog HDL.
- Verify signal transitions using a testbench.
- Analyze simulation waveforms using GTKWave.
- Synthesize the design using Yosys.
- Perform ASIC physical design using OpenLane/OpenROAD.
- Analyze cell utilization, timing reports, and final layout results.

3. Verilog RTL Code

File: "traffic_light.v"

`timescale 1ns/1ps

module traffic_light #(
    parameter GREEN_CYCLES  = 5,
    parameter YELLOW_CYCLES = 2,
    parameter RED_CYCLES    = 5
)(
    input wire clk,
    input wire reset,
    output reg red,
    output reg yellow,
    output reg green
);

    localparam GREEN  = 2'd0;
    localparam YELLOW = 2'd1;
    localparam RED    = 2'd2;

    reg [1:0] state;
    reg [31:0] counter;

    always @(posedge clk or posedge reset) begin
        if (reset) begin
            state   <= RED;
            counter <= 0;
        end else begin
            case (state)
                GREEN: begin
                    if (counter >= GREEN_CYCLES - 1) begin
                        state   <= YELLOW;
                        counter <= 0;
                    end else begin
                        counter <= counter + 1;
                    end
                end

                YELLOW: begin
                    if (counter >= YELLOW_CYCLES - 1) begin
                        state   <= RED;
                        counter <= 0;
                    end else begin
                        counter <= counter + 1;
                    end
                end

                RED: begin
                    if (counter >= RED_CYCLES - 1) begin
                        state   <= GREEN;
                        counter <= 0;
                    end else begin
                        counter <= counter + 1;
                    end
                end

                default: begin
                    state   <= RED;
                    counter <= 0;
                end
            endcase
        end
    end

    always @(*) begin
        red    = 0;
        yellow = 0;
        green  = 0;

        case (state)
            GREEN:  green  = 1;
            YELLOW: yellow = 1;
            RED:    red    = 1;
            default: red   = 1;
        endcase
    end

endmodule

4. Verilog Testbench

File: "traffic_light_tb.v"

`timescale 1ns/1ps

module traffic_light_tb;

    reg clk;
    reg reset;

    wire red;
    wire yellow;
    wire green;

    traffic_light #(
        .GREEN_CYCLES(5),
        .YELLOW_CYCLES(2),
        .RED_CYCLES(5)
    ) dut (
        .clk(clk),
        .reset(reset),
        .red(red),
        .yellow(yellow),
        .green(green)
    );

    initial clk = 0;
    always #5 clk = ~clk;

    initial begin
        $dumpfile("traffic_light.vcd");
        $dumpvars(0, traffic_light_tb);

        reset = 1;
        repeat (2) @(posedge clk);
        reset = 0;

        repeat (30) @(posedge clk);

        $display("Traffic Light Simulation Completed");
        $finish;
    end

endmodule

5. Simulation Commands

Run the following commands in Ubuntu from the project directory:

iverilog -g2012 -o traffic_sim traffic_light.v traffic_light_tb.v
vvp traffic_sim
gtkwave traffic_light.vcd

The simulation generates a VCD waveform file that can be inspected in GTKWave.

6. Synthesis Using Yosys

yosys -p "read_verilog traffic_light.v; hierarchy -top traffic_light; proc; opt; check; stat"

This command performs a basic synthesis check and displays statistics. Technology mapping for Sky130 requires the appropriate library and synthesis configuration.

7. Physical Design Flow

The following stages are intended to be performed using a configured OpenLane/OpenROAD flow:

1. RTL validation and synthesis.
2. Floorplanning and I/O planning.
3. Power distribution network (PDN) generation.
4. Standard-cell placement.
5. Clock-tree synthesis (CTS), when required.
6. Global and detailed routing.
7. Static timing analysis (STA).
8. Design-rule checking (DRC) and layout-versus-schematic (LVS), where supported.
9. GDSII layout generation.

Physical-design commands and configuration files depend on the installed OpenLane version and the selected Sky130 platform.

8. Tools and Technologies

- Verilog HDL
- Icarus Verilog
- GTKWave
- Yosys
- OpenLane / OpenROAD
- Sky130 PDK
- Ubuntu Linux
- Oracle VirtualBox

9. Expected Results

- Correct red, yellow, and green signal sequencing.
- Successful functional simulation and waveform generation.
- Synthesis statistics and standard-cell utilization reports.
- Floorplan, PDN, placement, CTS, and routing results.
- Timing reports and a GDSII layout, if all required physical-design stages complete successfully.

Actual results and screenshots should be added after each stage has been executed and verified.

10. Applications

- Road intersection traffic control.
- Digital control systems.
- FSM-based hardware design.
- ASIC design and verification learning.

11. Future Enhancements

- Pedestrian crossing control.
- Emergency-vehicle priority.
- Adaptive traffic timing based on sensor inputs.
- Power, performance, and area (PPA) optimization.

12. Conclusion

This project provides practical experience in Verilog RTL design, functional verification, logic synthesis, and ASIC physical design. It demonstrates how a digital traffic controller can progress from an RTL description toward a physical chip layout through a structured RTL-to-GDSII workflow.

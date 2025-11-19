CMOS Inverter Design – RTL to Layout Flow (Yosys + Magic VLSI + NGSpice)

This project demonstrates the complete VLSI digital design flow for a CMOS Inverter, starting from writing Verilog RTL, synthesizing into a gate-level netlist using Yosys, drawing the layout in Magic VLSI, extracting the SPICE netlist, and performing analog simulation with NGSpice.

 Project Overview

This project covers:


✔ Writing Verilog code for an inverter

✔ Synthesizing RTL into gate-level netlist using Yosys

✔ Creating layout using Magic VLSI

✔ Extracting SPICE netlist (.ext and .spice)

✔ Running transient simulation in NGSpice

✔ Understanding full custom + semi-custom design workflow


1. Inverter Verilog Code (RTL)
module inverter(a, y);
    input a;
    output y;
    assign y = ~a;
endmodule

2. Synthesizing Using Yosys
Create a Yosys Script (script.ys)
read_verilog inverter.v
synth -top inverter
write_verilog inverter_synth.v
show

Ubuntu Terminal Commands for Yosys

Run Yosys:

yosys


Inside Yosys run:

yosys> script.ys


Or directly:

yosys script.ys


To view gate-level:

show

 3. Layout in Magic VLSI
Launch Magic:
magic -T sky130A.tech


Inside Magic:

: load inverter.mag

Extract SPICE:
: extract all
: ext2spice


This generates:

inverter.spice

 4. NGSpice Simulation

Example NGSpice simulation file (inverter_sim.sp):

.include inverter.spice

Vdd vdd 0 1.8
Vin in 0 PULSE(0 1.8 0 1ns 1ns 5ns 10ns)

.tran 0.1ns 30ns
.control
run
plot v(in) v(out)
.endc
.end

 Ubuntu Terminal Commands for NGSpice

Run simulation:

ngspice inverter_sim.sp


To plot signals inside NGSpice:

plot v(in) v(out)

 Output Results

You should include images here, such as:

Gate-level schematic (from Yosys show)

Magic layout screenshot

NGSpice waveform (input vs output)

Example:

![Gate Level Schematic](images/gate_level.png)
![Magic Layout](images/layout.png)
![NGSpice Waveform](images/waveform.png)

Learnings

Complete CMOS inverter digital + analog flow

How RTL converts to standard cells

How layout extraction produces SPICE

CMOS operation validated through analog simulation

Tools Used
Tool	Purpose
Yosys	Synthesis (RTL → Gate-level netlist)
Magic VLSI	Layout design + extraction
NGSpice	SPICE simulation


AUTHOR 


VENKATESH DAMERA 


VLSI & EMBEDDED ENTHUSIAST

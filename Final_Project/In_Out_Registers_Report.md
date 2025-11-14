# Final Project: IN-OUT Registers for VSM

## Project Overview

In this project, we are using the muddlib library to create parts of a Very Simple Microprocessor (VSM). We are creating the In Register and Out Register which store the data for input and output until a signal is sent to enable the data to be processed. They are both registers that serve similar purposes in different ways, playing crucial roles in the microprocessor's data flow architecture.

## IN Register

The In Register uses tristates with enable pins to allow the input data to be sent to IB_BUS when an enable signal is triggered. This design allows the register to control when data is placed on the shared bus, implementing proper bus arbitration through high-impedance states.

### Schematic

The IN Register is implemented using tristate buffers that can drive the bus or enter a high-impedance state based on the EnableIn control signal. This allows multiple devices to share the same bus without interference.

<br><br>

<div align="center">
  <img src="imgs_and_videos/IN_Register_Logisim.png" width="600" alt="IN Register Schematic Logisim">
  <p><em>Figure 1: IN Register Schematic Implemented Using Tristate Buffers (Logisim)</em></p>
</div>

<br><br>

<div align="center">
  <img src="imgs_and_videos/IN_Register_Schematic.png" width="600" alt="IN Register Schematic">
  <p><em>Figure 2: IN Register Transistor-Level Schematic with Tristate Buffers</em></p>
</div>

<br><br>

### Simulation

The simulation demonstrates the proper operation of the tristate buffers under different enable conditions.

#### EnableIn = 1 (Driving the Bus)

When EnableIn is high (logic 1), the tristate buffers are active and drive the DataIn values onto the B bus outputs. This allows the IN Register to place data on the shared bus for other components to read.

<br><br>

<div align="center">
  <img src="imgs_and_videos/IN_Register_Sim.png" width="700" alt="IN Register Simulation Enable = 1">
  <p><em>Figure 3: SPICE Simulation of IN Register When EnableIn = 1 (Actively Driving Bus)</em></p>
</div>

<br><br>

#### Changing EnableIn (Showing High-Impedance Behavior)

This simulation shows the critical behavior of the tristate buffers as EnableIn toggles between 1 and 0. When EnableIn transitions to 0, the outputs enter a high-impedance (Hi-Z) state, effectively disconnecting from the bus and allowing other devices to use it without contention.

<br><br>

<div align="center">
  <img src="imgs_and_videos/IN_Register_Sim_at_Enable1.png" width="700" alt="IN Register Simulation with EnableIn toggling">
  <p><em>Figure 4: SPICE Simulation Demonstrating Tristate Operation When EnableIn Toggles</em></p>
</div>

<br><br>

### Layout

The physical layout implements four parallel tristate buffer structures, one for each bit of the 4-bit data path. The layout ensures proper routing of power, ground, and signal lines while maintaining compact design for integration into the larger VSM architecture.

<br><br>

<div align="center">
  <img src="imgs_and_videos/IN_Register_Layout.png" width="700" alt="IN Register Layout">
  <p><em>Figure 5: Completed IN Register Layout Showing Four Parallel Buffer Structures</em></p>
</div>

<br><br>

<div align="center">
  <img src="imgs_and_videos/IN_Register_Layout_3D.png" width="700" alt="IN Register 3D Layout">
  <p><em>Figure 6: 3D Rendering of IN Register Layout Showing Metal Layers and Interconnects</em></p>
</div>

<br><br>

## OUT Register

The OUT Register stores data from the IB_BUS and outputs it only when EnableOut is high. This register captures data on a clock edge and holds it until the next clock cycle, providing stable outputs for downstream logic.

### Initial Approach: D Flip-Flop from muddlib Library

Initially, muddlib D-Flip-Flops were used to implement the OUT Register. However, their two-phase clocking scheme caused double-triggering issues due to overlapping clocks.

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_muddlib_2phase.png" width="400" alt="muddlib D Flip-Flop">
  <p><em>Figure 7: mudLib Two-Phase D Flip-Flop Cell (ph2ph1 Configuration)</em></p>
</div>

<br><br>

### The Problem: Overlapping Clocks

The muddlib D flip-flop uses a master-slave architecture with two phases: PH1 and PH2. If these clock phases overlap (even when they are meant to be perfectly inverted), the flip-flop can trigger twice per clock cycle, causing incorrect operation and data corruption. This fundamental limitation necessitated the design of a custom D flip-flop.

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_masterSlave_Schematic.png" width="600" alt="New D FF Motivation Slide">
  <p><em>Figure 8: Master-Slave D Flip-Flop Architecture Showing Two-Phase Clocking</em></p>
</div>

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_muddlib_2phase_Schematic.png" width="600" alt="Muddlib DFF Schematic">
  <p><em>Figure 9: Detailed Schematic of mudLib Two-Phase D Flip-Flop</em></p>
</div>

<br><br>

### Custom D Flip-Flop Design

To solve the overlapping clock problem, a custom positive-edge-triggered D flip-flop was designed from scratch.

#### First Attempt: Level-Triggered D-Flip-Flop

The initial design attempted to create a D flip-flop using SR latch logic. This approach used NAND gates to implement the Set-Reset functionality with clock gating.

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_Logisim.png" width="600" alt="Custom SR-based DFF Logic">
  <p><em>Figure 10: Logic-Level Representation of First Custom D Flip-Flop Attempt Using SR Latch</em></p>
</div>

<br><br>

#### Transistor-Level Schematic

The schematic shows the transistor-level implementation with distinct sections:
- **Section A**: Master Latch (active on PH2)
- **Section B**: Slave Latch (active on PH1)  
- **Section C**: Logic between latches providing feedback path
- **Section D**: Inverters to create inverted clocks and buffered clock signals

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_Schematic.png" width="600" alt="Custom DFF Schematic">
  <p><em>Figure 11: Transistor-Level Schematic of Custom D Flip-Flop with Labeled Functional Blocks</em></p>
</div>

<br><br>

#### Adding Reset Logic

To add a reset capability without fully redesigning the D flip-flop, an AND gate was used to implement the reset functionality. The truth table ensures that when Reset is low (0), the D_in is forced to 0 regardless of the D input. Only when Reset is high (1) does D pass through to D_in.

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_Reset_Logic.png" width="600" alt="Custom DFF Reset Logic">
  <p><em>Figure 12: Reset Logic Added Using AND Gate to Enforce D_in Behavior</em></p>
</div>

<br><br>

#### Simulation – Level-Triggered Behavior

The simulation revealed that the first attempt was not edge-triggered as intended. Instead, it exhibited level-triggered behavior where the output Q reflected the D input at all times when the clock was high. This is not the desired behavior for a proper edge-triggered flip-flop.

<br><br>

<div align="center">
  <img src="imgs_and_videos/DFF_Sim.png" width="700" alt="Custom DFF Simulation Not Edge Triggered">
  <p><em>Figure 13: Simulation Showing That First Attempt Was Level-Triggered, Not Edge-Triggered</em></p>
</div>

<br><br>

#### Final Edge-Triggered Design

After identifying the level-triggered behavior issue, the design was revised to create a true positive-edge-triggered D flip-flop. This design captures the D input only on the rising edge of the clock and holds that value until the next rising edge.

<br><br>

<div align="center">
  <img src="imgs_and_videos/Edge_Triggered_DFF_Schematic.png" width="600" alt="Final Edge Triggered DFF">
  <p><em>Figure 14: Final Positive-Edge-Triggered Custom D Flip-Flop with Proper Edge Detection</em></p>
</div>

<br><br>

#### Final D-Flip-Flop Simulation

The final simulation confirms proper edge-triggered operation. The output Q changes only on the rising edge of the clock (Clk), capturing the value of D at that moment and holding it stable throughout the clock cycle.

<br><br>

<div align="center">
  <img src="imgs_and_videos/Edge_Triggered_DFF_Sim.png" width="700" alt="Final DFF Simulation">
  <p><em>Figure 15: SPICE Simulation of Final Edge-Triggered DFF Showing Correct Operation</em></p>
</div>

<br><br>

#### Layout of Final D-Flip-Flop

The layout implements the custom edge-triggered D flip-flop in physical form, carefully routing all transistor connections while minimizing area and ensuring proper operation at the target frequency.

<br><br>

<div align="center">
  <img src="imgs_and_videos/Edge_Triggered_DFF_Layout.png" width="700" alt="Final DFF Layout">
  <p><em>Figure 16: Physical Layout of Final Custom D Flip-Flop</em></p>
</div>

<br><br>

### OUT Register Implementation

With the custom D flip-flop successfully designed and verified, the OUT Register was implemented using both the original muddlib flip-flops and the new custom design for comparison.

#### OUT Register Schematic (muddlib)

The initial OUT Register implementation used four muddlib D flip-flops in parallel to create a 4-bit register. Each flip-flop stores one bit of data from the IB bus.

<br><br>

<div align="center">
  <img src="imgs_and_videos/OUT_Register_Logisim.png" width="600" alt="Out Register Schematic Using muddlib flops Logisim">
  <p><em>Figure 17: OUT Register Schematic Using mudLib Flip-Flops (Logisim Block Diagram)</em></p>
</div>

<br><br>

<div align="center">
  <img src="imgs_and_videos/OUT_Register_Schematic.png" width="600" alt="Out Register Schematic Using muddlib flops">
  <p><em>Figure 18: OUT Register Transistor-Level Schematic Using mudLib Flip-Flops</em></p>
</div>

<br><br>

#### Simulation

The SPICE simulation demonstrates the OUT Register operating with both EnableOut and Reset signals active. The register properly captures data from the IB bus (IB[3:0]) on the clock edge and drives the outputs (rOut[3:0]) when enabled. The reset functionality ensures all outputs can be cleared to a known state.

<br><br>

<div align="center">
  <img src="imgs_and_videos/OUT_Register_Sim.png" width="700" alt="Out Reg Simulation">
  <p><em>Figure 19: SPICE Simulation of OUT Register with EnableOut and Reset Active</em></p>
</div>

<br><br>

#### Layout

The final OUT Register layout integrates four custom D flip-flop cells in parallel, with proper routing for the 4-bit data path, clock distribution, enable, and reset signals. The layout is optimized for area efficiency while maintaining signal integrity.

<br><br>

<div align="center">
  <img src="imgs_and_videos/OUT_Register_Layout.png" width="750" alt="Out Register Layout">
  <p><em>Figure 20: OUT Register Physical Layout Using Four Custom DFF Cells</em></p>
</div>

<br><br>

<div align="center">
  <img src="imgs_and_videos/OUT_Register_Layout_3D.png" width="750" alt="Out Register 3D Layout">
  <p><em>Figure 21: 3D Rendering of OUT Register Layout Showing Complete Structure</em></p>
</div>

<br><br>

## Conclusion

This project successfully implemented both IN and OUT registers for the Very Simple Microprocessor (VSM) using the muddlib library. The IN Register provides controlled bus access through tristate buffers, while the OUT Register required the development of a custom edge-triggered D flip-flop to overcome limitations in the muddlib library's two-phase clocking scheme. Both registers were fully designed, simulated, and laid out, ready for integration into the complete VSM architecture.

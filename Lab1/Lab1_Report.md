# Lab 1 Report
## Introduction
This lab is the first lab in the VLSI Design Course, so it focusses on introducing Verilog as a Hardware Design Language as well as getting the student 
familiar with the FPGA board/Development Kit used (DE10-Lite). This overall goal is accomplished through several parts that build towards the final part
where a 7-segment display is used to display the word "HELLO".

## Part I
In this part of the lab, we are creating a simple 2 input, 1 select bit multiplexer. We created the mux_2_1 first on logisim to test and understand how 
it should work. Then, we created the multiplexer using HDL (in this case Verilog) in a way that switches can be used as inputs and LEDs can be used for 
the outputs. The code was finally uploaded to the DE10-Lite board to ensure that it functions correctly.

### LogiSim

Download Link: https://assignmentchef.com/product/solved-comp4300-lab-3
<br>
<span class="kksr-muted">Rate this product</span>

This lab develops the remaining datapath building blocks for the MIPS datapath. It will be combined with the MIPS control logic to make a working cpu in Lab 4.

Instructions

Develop VHDL for the following MIPS components. You should define an architecture for each of the entities given below. You should test each entity by developing simulation files for the entity. Your architecture should implement the functionality described in the text for each entity. To make the simulation results more readable, we will use a 32-bit datapath (both addr and data buses).

You should use the types from the dlx_types package you used in lab2, and the functions from bv_arithmetic as needed. The propagation delay through each unit should be 5 nanoseconds.

32-bit register . This will be used for the PC, NPC, A,B,Imm, ALUoutput, LMD, and IR registers. See Figure C.17 in textbook

<pre>entity dlx_register is     port(in_val: in dlx_word; clock: in bit; out_val: out</pre>

<pre>dlx_word);end entity dlx_register;</pre>

The register should be sensitive to all inputs. If clock is one, the value presentat in_val should be copied to out_val . When clock goes to zero, the output value is frozen until clock goes high again.

32-bit Two-way multiplexer Selects one of two thirty-two bit inputs based on whether the select bit is one or zero. This has no state; it is purely combinational logic.

<pre>entity mux is     port (input_1,input_0 : in dlx_word; which: in bit;</pre>

<pre>output: out dlx_word);end entity mux;</pre>

Sign extender Takes a 16-bit input, produces a 32-bit output whose lower 16 bits are the same as the input, and whose upper 16 bits are copies of the (sign) bit from the input. This is combinational logic and has no internal state or variables.

<pre>entity sign_extend is     port (input: in half_word; output: out dlx_word);</pre>

<pre>end entity sign_extend;</pre>

PC incrementer Adds 4 to its 32-bit input. Used to increment PC to create the value to put in NPC. An overflow is not indicated, you just wrap the address back around to zero (arithmetic mod 2**32). This is combinational logic and has no internal state.

<pre>entity add4 is    port (input: in dlx_word; output: out dlx_word);</pre>

<pre>end entity add4;</pre>

Register File This is a dual-ported register file for reads, single ported for writes. It hasa clock input that behaves just like the clock input on the single register defined above. Additionally it takes two 5-bit inputs regA and regB, each of which gives the address of the register whose 32-bit value is to be sent to the corresponding output port of the register file. There is a one-bit input Read_notwrite, that is set to a one do a read, a zero to do a write. Use the regA input as the number of the register to which the value in data_in is to be written for a write operation (read_notwrite = ‘0’).

<pre>entity regfile is     port (read_notwrite,clock : in bit;</pre>

<pre>           regA,rebB: in register_index;         data_in: in dlx_word;         dataA_out,dataB_out: out dlx_word         );</pre>
# Kartana3
A simple 8-bit CPU implemented completely in simple digital logic including 74XX series parts.

This is an implemenation of a simple 8-bit CPU design built using 74XX series digital logic on 2-layer PCBs.  The goal was to pick a simple instruction set that would allow for simple assembly language programs.  Due to the limited instructions set size realtive offsets and relocatable code is not possible.

## Instruction Set Architecture

The instruction set is a RISC-like load-store design with support for 16 general purpose registers.  The internal data path is 8-bits wide, as are the registers and the external data path.  The external memory architecure is a Harvard arcitecure with split program and data memory. The Program Counter is an 9-bit effective program counter supporting 512 bytes of program memory, and the external data memory is addressed with 8 bits of address supporting 256 bytes of data memory.

All instructions are a single size, 16 bits, requiring two bytes of program memory.   The CPU has a fixed two cycle fetch followed by a single cycle execution.  All instructions execute in a single cycle, netting a instructions/second rate 1/3 of the CPU clock rate.

Instruction Set:
!()/Docs/InstructionSetSummary.jpg


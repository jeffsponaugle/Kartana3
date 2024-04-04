# Kartana3
A simple 8-bit CPU implemented completely in simple digital logic including 74XX series parts.

This is an implemenation of a simple 8-bit CPU design built using 74XX series digital logic on 2-layer PCBs.  The goal was to pick a simple instruction set that would allow for simple assembly language programs.  Due to the limited instructions set size realtive offsets and relocatable code is not possible.

![](/images/IMG_7407.jpeg)

## Instruction Set Architecture

The instruction set is a RISC-like load-store design with support for 16 general purpose registers.  The internal data path is 8-bits wide, as are the registers and the external data path.  The external memory architecure is a Harvard arcitecure with split program and data memory. The Program Counter is an 9-bit effective program counter supporting 512 bytes of program memory, and the external data memory is addressed with 8 bits of address supporting 256 bytes of data memory.  There is also a dedicated 256 byte IO address space for devices.

All instructions are a single size, 16 bits, requiring two bytes of program memory.   The CPU has a fixed two cycle fetch followed by a single cycle execution.  All instructions execute in a single cycle, netting a instructions/second rate 1/3 of the CPU clock rate.

Instruction Set:

![](/Docs/InstructionSetSummary.jpg)

Most ALU operations are 3 operand, and there are not restrictions on those operands.  Each can be any of the 16 general purpose registers, and they do not need to be unique.

As an example:

`XOR R1,R1,R1`

would clear the R1 register, since and XOR against the same value results in zero.

The ALU operations ADD and SUB use the carry flag, and a side effect was added to the OR/XOR/AND/NOT operation to clear the carry flag.   You can use an instruction like OR R1,R1,R1 to make no changes except the CF clear.

Load and Store operations use either an immediate address or an address in a register, and a special LOADIO and STOREIO instruction writes to a dedicated IO address space.

The Shift operations are defined and partially decoded, but not in the physcial implementation.  The intention was to add this via a 5th PCB or via enhancements to the ALU PCB.

The Jump operation is absolute only, but there is space for a relative jump instruction not yet implemented.  With such a small instruction address space the relative jump is not needed.  Jump operations are flag driven, with two simple flag types: Carry and Zero.

All decode and operation logic is direct sequential logic with no microcode.  Microcode would be a slighty more compact implementation, but given the simple instruction set direct logic was straightfoward to design.  This also improved overall clock performance, which is operation at at least 2.5Mhz real clock rate.

## Physcial Implementation

The CPU is implemented on a total of 4 PCBs.

- A logic PCB that has all of the sequencing, decode, and signal generation.  This PCB could be replaced with a microcode implementation later if desired.

![](/images/IMG_7409.jpeg)

- An ALU PCB that implements the core ALU, which includes:
  +ADD 
  +SUB
  +AND
  +OR 
  +XOR   
  +NOT
  +PASS_THRU
![](/images/IMG_7412.jpeg)

- A register file PCB that implements 16x 8 bit registers. 

![](/images/IMG_7413.jpeg)

- A memory/clock PCB that has the system RAM, FLASH, LEDS, clock, reset button, and memory decoding logic.

![](/images/IMG_7407.jpeg)








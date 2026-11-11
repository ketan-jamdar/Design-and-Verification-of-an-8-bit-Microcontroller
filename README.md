# Design and Verification of an 8-bit Microcontroller using Verilog

## Project Summary :

Design and Verification of 8 bit microcontroller using Verilog. Goal is to design custom microcontroller architecture with its own instruction set & verified its functionality through simulation in Vivado.

Architecture have three main parts: Datapath, Control unit & Memory system.

Datapath includes ALU, Accumulator, Program Counter (PC), Instruction Resistor (IR) & Data Register (DR).

Control unit is based on FSM & operates through four states that are LOAD, FETCH, DECODE & EXECUTE. In LOAD state we load instruction to Program Memory, during FETCH the instruction is loaded into Instruction Register. In DECODE the control signal is generated & in EXECUTE the ALU performs the required operation.

The ALU supports 14 operations such as AND, OR, XOR, ADD, SUB, shift, rotate & increment/decrement. Each instruction is 12 bit wide & classified M/S/I type for memory, immediate & special operations.

For verification I wrote multiple test programs in a binary file & loaded them into program memory. I simulated the design in Vivado & verified correct instruction execution by observing the waveforms of program counter, accumulator & status flag.

## Features

- Designed a custom 8-bit Harvard Architecture Microcontroller
- Developed in Verilog HDL
- 12-bit custom instruction format
- 4-stage instruction execution:
  - Load
  - Fetch
  - Decode
  - Execute
- FSM-based Control Unit
- 14 ALU operations
- Separate Program Memory and Data Memory
- Binary instruction program loading using `$readmemb`
- Functional verification using multiple test programs
- Simulation performed in QuestaSim

## Processor Architecture

The microcontroller consists of three major subsystems:

- Datapath
- Control Unit
- Memory System

<img width="1308" height="1202" alt="Image" src="https://github.com/user-attachments/assets/8d937be3-9908-4ab7-afc8-00a4960a5a0d" />

## RTL Module Hierarchy

MicroController

│

├── ALU

├── Control_Logic

├── Program Memory

├── Data Memory

├── Program Counter

├── Instruction Register

├── Data Register

├── Accumulator

├── Status Register

├── Adder

└── MUX1 / MUX2

## Module Description

| Module | Description |
|--------|-------------|
| **ALU** | Performs arithmetic and logical operations. |
| **Control Logic** | Generates control signals based on the current state and instruction. |
| **Program Counter (PC)** | Holds the address of the next instruction to be executed. |
| **Program Memory (PMem)** | Stores the program instructions. |
| **Data Memory (DMem)** | Stores data used during program execution. |
| **Instruction Register (IR)** | Holds the currently fetched instruction. |
| **Data Register (DR)** | Stores data read from the data memory. |
| **Accumulator (ACC)** | Main working register that stores ALU operation results. |
| **Status Register (SR)** | Stores processor status flags: Zero (Z), Carry (C), Sign (S), and Overflow (O). |
| **MUX1 / MUX2** | Select the appropriate input source for the Program Counter and ALU based on control signals. |

## Instruction Set
| Opcode | Operation | Description |
|:------:|:---------:|-------------|
| `0000` | **ADD**   | Addition |
| `0001` | **SUB**   | Subtraction |
| `0010` | **MOV**   | Move |
| `0011` | **LOAD**  | Load |
| `0100` | **STORE** | Store |
| `0101` | **AND**   | Bitwise AND |
| `0110` | **OR**    | Bitwise OR |
| `0111` | **XOR**   | Bitwise XOR |
| `1000` | **INC**   | Increment |
| `1001` | **DEC**   | Decrement |
| `1010` | **ROL**   | Rotate Left |
| `1011` | **ROR**   | Rotate Right |
| `1100` | **SHL**   | Shift Left |
| `1101` | **SHR**   | Shift Right |

## Execution Flow (FSM)

Each instruction needs 3 clock cycles to finish, i.e. FETCH stage, DECODE stage, and EXECUTE stage. Note that it is not pipelined. Together with the initial LOAD state, it can be considered as an FSM of 3 states (technically 4 states).
<img width="1536" height="1024" alt="Image" src="https://github.com/user-attachments/assets/888042f1-f264-42cd-b738-f1c53fda21d0" />

### States

1. **LOAD (Initial State):** Load program to Program Memory, which takes **1 cycle per instruction** loaded.
2. **FETCH (First Cycle):** Fetch current instruction from Program Memory.
3. **DECODE (Second Cycle):** Decode instruction to generate control logic and read Data Memory for operand.
4. **EXECUTE (Third Cycle):** Execute instruction.

## Test Programs

To verify the functionality of the 8-bit Microcontroller, four test programs were developed. Each program focuses on validating a specific group of instructions, ensuring correct execution of memory access, arithmetic, logical, and shift/rotate operations.

**Test Program Summary**
|  **Program**  | **Purpose**                 |
| :-----------: | --------------------------- |
| **Program 1** | Memory Operations           |
| **Program 2** | Arithmetic Operations       |
| **Program 3** | Logic Operations            |
| **Program 4** | Shift and Rotate Operations |

## Tools Used

- Xilinx Vivado (RTL Coding)
- QuestaSim (Simulation Waveforms)
- GitHub

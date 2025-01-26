# samsung-riscv
The program is based on the RISC-V architecture and uses open-source tools for VLSI chip design and RISC-V.

## Basic Details

*Name:* Rohan N D

*College:* Vidyavardhaka College of Engineering

*Email ID:*rohanndbrigade@gmail.com

*GitHub Profile:* rohan004

*LinkedIN Profile:* Rohan N D


<details>
<summary> <b>Task 1:</b></summary>
<br>
Task is to refer to C based and RISCV based lab videos and execute the task of compiling the C code using gcc and riscv compiler
	
*C and RISC-V Based Labs*

This repository demonstrates the processes involved in compiling C programs and generating assembly code using both a standard GCC compiler and a RISC-V GCC compiler. It includes comprehensive steps and explanations to guide users through each stage of the compilation and debugging workflow.

*C Language-Based Lab*

Steps to Compile a .c File on Your Machine:

1. Open the bash terminal and navigate to the directory where you want to create your file.
2. Use the following command to create and edit a new .c file:
   sh
   gedit sum_1ton.c
![sum1ton_code_snippet](https://github.com/user-attachments/assets/f0286e5a-c777-492b-a4a7-f858315aec9f)

**Steps to Compile a .c File :**
 sh
 gcc sum_1ton.c
 ./a.out

**Compilation and execution complete.**

![sum1ton_output]


**RISC-V Based Lab**

### Steps to Compile Using RISC-V GCC Compiler:
1. Ensure the RISC-V GCC compiler is installed and accessible on your system.
2. Verify the .c file contents using the cat command:
sh
cat sum_1ton.c

![cat_sum1ton](https://github.com/user-attachments/assets/804de266-d64b-4bfc-82e5-d001f9e754cd)

4. Compile the C program for RISC-V architecture using:
 sh
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum_1ton.o sum_1ton.c
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c

![O1 and Ofast](https://github.com/user-attachments/assets/463e27c5-465e-4dd3-ae1c-899aae08c371)


5. Disassemble the object file to view its assembly code using:
 sh
riscv64-unknown-elf-objdump -d sum_1ton.o

6. Use /main in the terminal to locate the main function in the assembly output.
![assembly_code_snippet](https://github.com/user-attachments/assets/98ebc243-65f5-441a-8e8e-dc1353a18050)

**Explanation of Commands and Options:**
1. -mabi=lp64: Specifies the Application Binary Interface (ABI) for 64-bit integers, pointers, and long data types, suitable for 64-bit RISC-V architecture.

2. -march=rv64i: Indicates the 64-bit RISC-V base integer instruction set architecture.

3. -O1: Enables basic optimization for better performance without significantly increasing compilation time.
  
4. -Ofast: Focuses on maximizing performance by enabling aggressive optimizations, potentially at the cost of standard compliance.

5. riscv64-unknown-elf-objdump: A tool for disassembling RISC-V binaries to examine the code structure and debug it effectively.

</details>

<details>
<summary><b>Task 2:</b></summary>
<br>
	
**Debugging with SPIKE: Comparing -O1 and -Ofast Optimizations**

**-O1:** A moderate optimization for balanced performance.

**-Ofast:** A high-speed optimization that prioritizes performance over strict standards

**add.c File**
![sum code](https://github.com/user-attachments/assets/8989da87-e34d-4330-af71-683b478b9642)

Commands:

riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum.o sum.c
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum.o sum.c

![Debugging O1](https://github.com/user-attachments/assets/bbe095b5-3675-4d59-990a-fd950a0b3cca)

![Debugging Ofast](https://github.com/user-attachments/assets/507818d0-2605-4473-a0ce-182c81f88900)


**Running on SPIKE**

Commands:

spike pk sum.o
spike -d pk sum.o


Objdump:

riscv64-unknown-elf-objdump -d sum.o

![Objdump -O1](https://github.com/user-attachments/assets/057054e4-16f8-42b0-a7cb-d51486dfa856)

![Objdump -Ofast](https://github.com/user-attachments/assets/b7874894-8ed7-42a7-907d-deee09188ec4)


</details>
</details>
</details>
<details>
<summary><b>Task 3:</b> The task is to determine the instruction type for each of the provided instructions and provide their corresponding 32-bit instruction codes in the appropriate format</summary>

# Understanding RISC-V and Its Instruction Formats

## What is RISC-V?
RISC-V is an open-source Instruction Set Architecture (ISA) that enables developers to design processors tailored to specific applications. Based on Reduced Instruction Set Computer (RISC) principles, RISC-V represents the fifth generation of processors built on this concept. Its open and free nature means developers can utilize RISC-V without purchasing licenses, making it a compelling alternative to proprietary processor technologies.

## Instruction Formats in RISC-V
The instruction format of a processor defines how machine language instructions are structured for execution. These instructions are composed of binary data (0s and 1s), each segment providing details about data location and operations to be performed. In RISC-V, there are six primary instruction formats:

1. **R-format**
2. **I-format**
3. **S-format**
4. **B-format**
5. **U-format**
6. **J-format**
<img width="772" alt="instructions_types" src="https://github.com/user-attachments/assets/7ca6b3ea-bd59-4419-8410-1e14e40e911e" />


---

### 1. R-type Instruction
R-type (Register-type) instructions operate on registers rather than memory locations. These are used for arithmetic and logical operations. Each instruction is 32 bits and divided into six fields:

#### Structure:

| Field Name | Size  | Description                            |
|------------|-------|----------------------------------------|
| Opcode     | 7 bits| Determines the instruction type        |
| rd         | 5 bits| Destination register                  |
| func3      | 3 bits| Specifies the type of operation       |
| rs1        | 5 bits| First source register                 |
| rs2        | 5 bits| Second source register                |
| func7      | 7 bits| Additional operation specification    |

#### Example: ADD r9, r2, r5
- **Operation:** Adds values in registers r2 and r5, storing the result in r9.
- **Field Breakdown:**

  - Opcode: `0110011`
  - rd (Destination): `r9` -> `01001`
  - rs1 (Source 1): `r2` -> `00010`
  - rs2 (Source 2): `r5` -> `00101`
  - func3: `000`
  - func7: `0000000`
- **32-bit Instruction:** `0000000_00101_00010_000_01001_0110011`


#### Example: XOR r10, r1, r4
- **Operation:** XOR operation between r1 and r4, result in r10.
- **Field Breakdown:**

  - Opcode: `0110011`
  - rd (Destination): `r10` -> `01010`
  - rs1 (Source 1): `r1` -> `00001`
  - rs2 (Source 2): `r4` -> `00100`
  - func3: `100`
  - func7: `0000000`
- **32-bit Instruction:** `0000000_00100_00001_100_01010_0110011`


#### Example: SLT r11, r2, r4
- **Operation:** Sets r11 to 1 if r2 < r4; otherwise, sets r11 to 0.
- **Field Breakdown:**

  - Opcode: `0110011`
  - rd (Destination): `r11` -> `01011`
  - rs1 (Source 1): `r2` -> `00010`
  - rs2 (Source 2): `r4` -> `00100`
  - func3: `010`
  - func7: `0000000`
- **32-bit Instruction:** `0000000_00100_00010_010_01011_0110011`

![r type](https://github.com/user-attachments/assets/33357c39-806e-4d2f-9158-cd204120dcd8)


---

### 2. I-type Instruction
I-type (Immediate-type) instructions use a register and an immediate (constant) value. These are typically used for load and immediate operations.

#### Structure:

| Field Name | Size  | Description                            |
|------------|-------|----------------------------------------|
| Opcode     | 7 bits| Determines the instruction type        |
| rd         | 5 bits| Destination register                  |
| func3      | 3 bits| Specifies the type of operation       |
| rs1        | 5 bits| Source register                       |
| imm[11:0]  | 12 bits| Immediate value                      |

#### Example: ADDI r12, r4, 5
- **Operation:** Adds immediate value 5 to the value in r4 and stores it in r12.
- **Field Breakdown:**
  - Opcode: `0010011`
  - rd (Destination): `r12` -> `01100`
  - rs1 (Source): `r4` -> `00100`
  - imm[11:0] (Immediate): `000000000101`
  - func3: `000`
- **32-bit Instruction:** `000000000101_00100_000_01100_0010011`

![i type](https://github.com/user-attachments/assets/76a06842-0672-46d8-b50e-c538c6f63c99)


---

### 3. S-type Instruction
S-type (Store-type) instructions store register values into memory locations.

#### Structure:

| Field Name | Size  | Description                            |
|------------|-------|----------------------------------------|
| Opcode     | 7 bits| Determines the instruction type        |
| rs1        | 5 bits| Base address register                 |
| rs2        | 5 bits| Source register                       |
| imm[11:5]  | 7 bits| Upper immediate value                  |
| imm[4:0]   | 5 bits| Lower immediate value                  |
| func3      | 3 bits| Specifies the type of operation       |

#### Example: SW r3, 2(r1)
- **Operation:** Stores the value in r3 into the memory at the address `r1 + 2`.
- **Field Breakdown:**
  - Opcode: `0100011`
  - rs1 (Base Address): `r1` -> `00001`
  - rs2 (Source): `r3` -> `00011`
  - imm[11:5] (Upper Immediate): `0000000`
  - imm[4:0] (Lower Immediate): `00010`
  - func3: `010`
- **32-bit Instruction:** `0000000_00011_00001_010_00010_0100011`

![s type](https://github.com/user-attachments/assets/a6210bc8-77c1-424d-a6e0-ada39b5189da)


---

### 4. B-type Instruction
B-type (Branch-type) instructions handle branching based on conditions.

#### Structure:

| Field Name | Size  | Description                            |
|------------|-------|----------------------------------------|
| Opcode     | 7 bits| Determines the instruction type        |
| rs1        | 5 bits| Source register 1                      |
| rs2        | 5 bits| Source register 2                      |
| imm[12|10:5|4:1|11] | 13 bits| Branch offset                      |
| func3      | 3 bits| Specifies the condition for branching |

#### Example: BNE r0, r1, 20
- **Operation:** Branches to the address `PC + 20` if r0 is not equal to r1.
- **Field Breakdown:**
  - Opcode: `1100011`
  - rs1: `r0` -> `00000`
  - rs2: `r1` -> `00001`
  - imm[12|10:5|4:1|11]: `0000010100`
  - func3: `001`
- **32-bit Instruction:** `0000000_00001_00000_001_10100_1100011`

#### Example: BEQ r0, r0, 15
- **Operation:** Branches to the address `PC + 15` if r0 equals r0 (always true).
- **Field Breakdown:**
  - Opcode: `1100011`
  - rs1: `r0` -> `00000`
  - rs2: `r0` -> `00000`
  - imm[12|10:5|4:1|11]: `000001111`
  - func3: `000`
- **32-bit Instruction:** `0000000_00000_00000_000_01111_1100011`

![b type](https://github.com/user-attachments/assets/31c67705-07f0-4d1d-86e0-2c0d8e3e2e78)

---

### 5. U-type Instruction
U-type (Upper Immediate) instructions load immediate data into the destination register.

#### Structure:

| Field Name | Size  | Description                            |
|------------|-------|----------------------------------------|
| Opcode     | 7 bits| Determines the instruction type        |
| rd         | 5 bits| Destination register                  |
| imm[31:12] | 20 bits| Upper immediate value                  |

![u type](https://github.com/user-attachments/assets/d5223eda-40fd-4418-8860-39f350330311)


---

### 6. J-type Instruction
J-type (Jump-type) instructions implement jump operations, often used for loops.

#### Structure:

| Field Name | Size  | Description                            |
|------------|-------|----------------------------------------|
| Opcode     | 7 bits| Determines the instruction type        |
| rd         | 5 bits| Destination register                  |
| imm[20|10:1|11|19:12] | 20 bits| Jump offset                        |

![j type](https://github.com/user-attachments/assets/f9841148-7b72-42c1-adea-3a9e2068d621)


---


This repository contains a list of 15 unique RISC-V instructions extracted from the assembly code along with their corresponding 32-bit instruction codes. These instructions cover different instruction formats, such as **U-type**, **I-type**, **J-type**, **B-type**, and **R-type**.


# RISC-V Instructions

This README contains a table of 15 unique RISC-V instructions, their machine codes, opcodes, formats, and instruction binaries.

| **Instruction**                 | **Opcode**  | **Format**   | **Machine Code** | **Instruction Binary**                        |
|----------------------------------|-------------|--------------|------------------|-----------------------------------------------|
| **lui a0, 0x21** (Load Upper Immediate) | 0110111     | U-type       | 0x00021537       | 00000000001000010001000000010011             |
| **li a3, 15** (Load Immediate)       | 0010011     | I-type       | 0x00f00693       | 00000000011100000000011001001111             |
| **addi a0, a0, 352** (Add Immediate) | 0010011     | I-type       | 0x16050513       | 00010110000001010000010100010011             |
| **j 103f4** (Jump)                  | 1101111     | J-type       | 0x3300006f       | 00000011001100000000000001101111             |
| **auipc a5, 0xffff0** (Add Upper Immediate to PC) | 0010111     | U-type       | 0xffff0797       | 11111111111100000111000010010111             |
| **addi a5, a5, -200** (Add Immediate) | 0010011     | I-type       | 0xf3878793       | 11110000100001111000011100111001             |
| **beqz a5, 100e0** (Branch if Equal Zero) | 1100011     | B-type       | 0x00078863       | 00000000000001111000100001100011             |
| **auipc a0, 0x0** (Add Upper Immediate to PC) | 0010111     | U-type       | 0x00000517       | 00000000000000000000000001010111             |
| **j 1019c** (Jump)                  | 1101111     | J-type       | 0x0c00006f       | 00000000110000000000000001101111             |
| **addi a0, gp, 1904** (Add Immediate) | 0010011     | I-type       | 0x11050513       | 00010001000001010000010100110011             |
| **sub a2, a2, a0** (Subtract)       | 0110011     | R-type       | 0x40a60633       | 01000000101001100000011000110011             |
| **ret** (Pseudo-instruction for `jalr x0, x1, 0`) | 1100111     | I-type       | 0x00008067       | 00000000000000000000000001100111             |
| **auipc gp, 0x13** (Add Upper Immediate to PC) | 0010111     | U-type       | 0x00013197       | 00000000000000010011000110010111             |
| **andi a1, a1, 0xFF** (Logical AND Immediate) | 0010011     | I-type       | 0x00a30313       | 00000000001000110000001100010011             |
| **mul a2, a3, a4** (Multiply)       | 0110011     | R-type       | 0x00b30333       | 00000000001000110011000010010011             |

</details>
<details>
<summary><b>Task 4:</b>By making use of RISCV Core: Verilog Netlist and Testbench, perform an experiment of Functional Simulation and observe the waveforms</summary>
<br>
	
**4. FUNCTIONAL SIMULATION**

**4.1 About iverilog and gtkwave**
- Icarus Verilog is an implementation of the Verilog hardware description language.
- GTKWave is a fully featured GTK+ v1. 2 based wave viewer for Unix and Win32 which reads Ver Structural Verilog Compiler generated AET files as well as standard Verilog VCD/EVCD files and allows their viewing.

### 4.2 Installing iverilog and gtkwave

- **For Ubuntu**

 Open your terminal and type the following to install iverilog and GTKWave
 ```
 $   sudo apt get update
 $   sudo apt get install iverilog gtkwave
 ```

- **To clone the repository and download the netlist files for simulation , enter the following commands in your terminal.**

 ```
 $ git clone https://github.com/vinayrayapati/iiitb_rv32i
 $ cd iiitb_rv32i
 ```
- **To simulate and run the verilog code , enter the following commands in your terminal.**

```
$ iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
$ ./iiitb_rv32i
```
- **To see the output waveform in gtkwave, enter the following commands in your terminal.**

`$ gtkwave iiitb_rv32i.vcd`

**4.3 The output waveform**

 The output waveform showing the instructions performed in a 5-stage pipelined architecture.
 
 Instruction 1:add r6,r2,r1
 
 ![ADD](https://github.com/user-attachments/assets/586412bd-efe8-4062-a902-e42cae6c7f43)


 Instruction 2:sub r7,r1,r2
 
![SUB](https://github.com/user-attachments/assets/a0eceee9-4a6f-4050-89d5-c2923509551d)


 Instruction 3:and r8,r1,r3
 
![AND](https://github.com/user-attachments/assets/184e9459-0326-46e2-b6c7-dd081636bfe0)


 Instruction 4:or r9,r2,r5
 
![OR](https://github.com/user-attachments/assets/b2da64c3-3a97-4dc0-8901-1573d97385a7)


 Instruction 5:xor r10,r1,r4
 
![XOR](https://github.com/user-attachments/assets/184e33be-f1d7-4e91-83b2-64080e9fc653)


 Instruction 6:slt r11,r2,r4
 
![SLT](https://github.com/user-attachments/assets/293ebe8e-d997-4e9f-8812-5015c8827596)


 Instruction 7:addi r12,r4,5
 
![ADDI](https://github.com/user-attachments/assets/1441f388-533d-4d00-b904-2cd7647c8737)


 Instruction 8:lw r13,r1,2
 
![LW](https://github.com/user-attachments/assets/5db2f15c-7cf8-496b-af93-89649c25ae43)

 Instruction 9:beq r0,r0,15

![BEQ](https://github.com/user-attachments/assets/43fc1344-5bbc-4c33-9d1b-2f1f2d6b4234)


 Full 5-stage instruction pipeline and pc-increment description Waveform
 
![FULL 5 STAGE](https://github.com/user-attachments/assets/719d2d6a-88a6-4521-9935-4f5c6d31fb13)

</details>


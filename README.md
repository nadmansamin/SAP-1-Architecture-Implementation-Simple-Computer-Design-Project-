# SAP-1-Architecture-Implementation-Simple-Computer-Design-Project-

This repository contains the schematic, design files, and circuit simulation for an **8-bit Computer System based on the Simple-As-Possible (SAP-1) Architecture**[cite: 7]. Developed as part of the Digital Electronics Lab (EEE 4308) course at the Islamic University of Technology (IUT), the system is built entirely using discrete TTL logic ICs, timers, and static memory in Proteus[cite: 7].

Beyond the base SAP-1 specification, our design extends the hardware capabilities to support **bitwise logic operations (AND, OR)** and **non-sequential control flow (`JMP`)** using an expanded microprogrammed control unit[cite: 7].

Key Features & Hardware Modifications

- **Dual-Mode Clock Unit:** Features a manual single-step mode (monostable 555 timer) and an auto-clock mode with full software/hardware execution halting capabilities (`HLT`)[cite: 7].
- **Synchronous Program Counter:** Upgraded from standard ripple counter implementations to a 4-bit synchronous loading counter to reliably support target jump addresses[cite: 7].
- **$16 \times 8$ Main Memory Array:** Designed using dual 74LS189 static RAM ICs paired with an integrated Read/Write logic state machine and Memory Address Register (MAR)[cite: 7].
- **Extended ALU Architecture:** Extended the standard adder/subtractor circuit with dedicated logic function paths via a 74HC139 demultiplexer routing to AND and OR gate arrays[cite: 7].
- **Microprogrammed Control Unit:** EPROM-based ($27\text{C}64$) instruction decoding driving a 14-bit control word across T-states ($T_1$ through $T_6$)[cite: 7].
- **Visual Output Register:** 8-bit output display interface leveraging 74LS173 registers and tri-state bus drivers[cite: 7].

Extended Instruction Set Architecture (ISA)

| Mnemonic | Opcode | Description | Microcode Steps (T-States)[cite: 7] |
| :--- | :---: | :--- | :--- |
| **LDA** | `0000` | Load value from RAM into Accumulator | $T_2$: IO \| MI, $T_3$: RO \| AI[cite: 7] |
| **ADD** | `0001` | Add RAM value to Accumulator | $T_2$: IO \| MI, $T_3$: RO \| BI, $T_4$: EO \| AI[cite: 7] |
| **SUB** | `0010` | Subtract RAM value from Accumulator | $T_2$: IO \| MI, $T_3$: RO \| BI, $T_4$: EO \| AI \| SU[cite: 7] |
| **OUT** | `1110` | Output Accumulator contents to visual register | $T_2$: AO \| OI[cite: 7] |
| **HLT** | `1111` | Stop internal clock generation | $T_2$: HLT[cite: 7] |
| **AND** *(Extended)* | `0100` | Perform bitwise AND with RAM operand | $T_2$: IO \| MI, $T_3$: RO \| BI, $T_4$: EO \| AI \| AN[cite: 7] |
| **OR** *(Extended)* | `0101` | Perform bitwise OR with RAM operand | $T_2$: IO \| MI, $T_3$: RO \| BI, $T_4$: EO \| AI \| OR[cite: 7] |
| **JMP** *(Extended)* | `0111` | Unconditional jump to operand memory address | $T_2$: IO \| LP[cite: 7] |



Key IC Components

- **Logic Gates & Decoding:** 74HC08 (AND), 74HC32 (OR), 74HC04 (NOT), 74HC86 (XOR), 74HC139 (2-to-4 Decoder)[cite: 7]
- **Registers & Counters:** 74LS173 (4-bit D-Register), 74LS193 (Synchronous Counter)[cite: 7]
- **Bus Transceivers & Buffers:** 74LS245 (8-bit Octal Bus Transceiver), 74126 (Tri-State Buffers)[cite: 7]
- **ALU & Storage:** 74LS283 (4-bit Binary Adder), 74LS189 (Static RAM), 27C64 (CMOS EPROM)[cite: 7]
- **Timing:** NE555 Precision Timers[cite: 7]

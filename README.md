# Bare-Metal RISC-V SoC & Arcade Game

**Status:** In Development (Phase 1: CPU Core)

## Overview

This project is a complete, custom-built 32-bit RISC-V System-on-Chip (SoC) designed from scratch in Verilog. Synthesized on a Sipeed Tang Nano 9K FPGA, the custom silicon is designed specifically to execute a bare-metal C arcade game (like Pong/Snake) using a custom memory-mapped HDMI video controller.

By building the entire vertical stack—from the physical logic gates up to the C application code—this project explores instruction set architecture, pipelining, clock domain crossing, and bare-metal software development.

## Tech Stack & Toolchain

### Hardware

* **Board:** Sipeed Tang Nano 9K (Gowin GW1NR-9 FPGA)
* **Display:** Standard 1080p Monitor via onboard HDMI port
* **Inputs:** Breadboard, jumper wires, and tactile pushbuttons wired to GPIO

### Software & Verification

* **HDL:** Verilog / SystemVerilog
* **Simulation:** Verilator / Icarus Verilog + GTKWave
* **Synthesis & Routing:** OSS-CAD-Suite (Yosys, Nextpnr, Apicula) / Gowin EDA
* **Application Language:** C and RISC-V Assembly (RV32I)
* **Compiler:** RISC-V GNU Compiler Toolchain (`riscv-none-elf-gcc`)

## System Architecture

### 1. Hardware Architecture (The SoC)

* **CPU Core:** 5-stage pipelined RV32I architecture (Fetch, Decode, Execute, Memory, Write-Back).
* **Memory subsystem:** Block RAM (BRAM) instantiated for Instruction Memory (ROM) and Data Memory (RAM).
* **Video Controller:** Custom RTL to generate HDMI sync timings and draw memory-mapped pixels to the screen.
* **I/O Peripherals:** Hardware debouncing modules for the physical button inputs.

### 2. Software Architecture (The Game)

* **Bare-Metal:** No Operating System. The C code executes directly on the custom hardware.
* **Memory-Mapped I/O:** The game writes directly to specific physical memory addresses that the Verilog hardware interprets as screen pixels.
* **Infinite Loop:** The software utilizes a single `while(1)` polling loop to read button states, update game physics, and draw the frame.

## Project Roadmap

* [ ] **Phase 1: The Processor Core**
  * [ ] Implement the Arithmetic Logic Unit (ALU).
  * [ ] Build the Register File and Program Counter.
  * [ ] Implement the 5-stage pipeline and instruction decoder.
  * [ ] Write SystemVerilog testbenches and verify with GTKWave.
  * [ ] *Milestone:* Blink an LED via RISC-V machine code loaded into ROM.

* [ ] **Phase 2: The Peripherals & SoC Integration**
  * [ ] Write the HDMI/VGA video controller in Verilog.
  * [ ] Implement memory-mapped I/O routing to connect the CPU to the video controller.
  * [ ] Wire up and debounce physical GPIO buttons.
  * [ ] *Milestone:* Change the monitor screen color using C code.

* [ ] **Phase 3: The Software Application**
  * [ ] Set up the RISC-V GCC cross-compiler.
  * [ ] Write the arcade game logic (Pong/Snake) in C.
  * [ ] Compile the game to a `.hex` file and load it into the FPGA bitstream.
  * [ ] *Milestone:* Play the game!

## Verification & Results

* **Phase 1 (CPU Core):** [Placeholder for ALU/Pipeline test results and GTKWave screenshots]
* **Phase 2 (Peripherals):** [Placeholder for HDMI timing verification and button debounce testing]
* **Phase 3 (Software):** [Placeholder for bare-metal C execution results]

## How to Build & Run (Coming Soon)


1. **Simulate the CPU:** `make simulate`
2. **Compile the Game:** `make software`
3. **Flash the FPGA:** `make flash`

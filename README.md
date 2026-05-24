# The Professor's Hero 🏰🎓
### FPGA-Based Interactive Educational Puzzle Game
**Hacettepe University | Department of Electrical & Electronics Engineering** **ELE432 Advanced Digital Design (Spring 2026) Final Project**

---

## 📌 Project Overview
**The Professor's Hero** is a fully standalone, hardware-driven educational puzzle game designed and synthesized entirely from scratch on the **Terasic DE1-SoC (Altera Cyclone V)** platform using **SystemVerilog**. 

Inspired by Vladimir Tumanov’s educational book *"Saving the Queen"*, this project bridges abstract Boolean algebra and digital logic concepts with deterministic real-time hardware execution. The player navigates a 5x3 grid-based matrix (castle) to solve structural hardware-centric quizzes and bypass boolean gating paths in order to rescue a captured professor. The entire architecture runs natively on the FPGA fabric without any microprocessor or soft-core reliance, achieving **zero operational latency**.

---

## 🛠️ Hardware & Peripheral Mapping
To ensure robust interaction and an error-free diagnostic testing environment, custom hardware label interfaces were designed for the DE1-SoC board layout:

| Hardware Component | System Mapping | Functionality Description |
| :--- | :--- | :--- |
| **KEY[3:0]** | Movement Vectors | Tactile buttons mapped for 2D grid navigation (Up, Down, Left, Right). |
| **SW[4:0]** | Multiple-Choice Input | 5-bit one-hot encoded selection vector representing quiz options **[A, B, C, D, E]**. |
| **SW[5]** | Binary Charge Modulator | Dynamically toggles the player character's logical state (`0` or `1`). |
| **SW[9]** | System Reset | Asynchronous master hardware reset trigger. |
| **VGA Output** | Triple 8-bit Video DAC | Streams a real-time 640x480 @ 60Hz visual matrix via the onboard ADV7123 chip. |
| **LEDR[9:0]** | Status Monitors | Hardware status verification and passcode alignment displays. |

---

## 🏗️ Architecture & Core Modules
The design is structurally modularized to enforce high concurrent processing efficiency across the FPGA fabric:

### 1. Master Control Unit (Finite State Machine - FSM)
A highly deterministic, synchronous FSM controls the global operational states:
* `STATE_INTRO`: Renders the structural narrative introduction and opening splash screen assets.
* `STATE_GAME`: Handles active map exploration, coordinate tracking, grid collision boundaries, and real-time obstacle processing.
* `STATE_GATE_SCREEN`: Triggered upon advanced node collision. Freezes gameplay and spawns the blue procedural mathematical formula panel.
* `STATE_VICTORY`: Halts all operational timers and flashes the absolute performance score benchmark on a green triumph background.

### 2. High-Precision VGA Timing Controller
Generates synchronous display sweeping waveforms under strict VESA standards using a precise pixel clock divided down to **25.175 MHz**:
* **Horizontal Line Profile:** 640 Active Pixels + 16 Front Porch + 96 Sync Pulse + 48 Back Porch = 800 Total Ticks.
* **Vertical Frame Profile:** 480 Active Lines + 10 Front Porch + 2 Sync Pulse + 33 Back Porch = 525 Total Ticks.

### 3. Procedural Graphics Engine
To prevent heavy block RAM (M10K) memory inflation associated with massive static pre-rendered bitmaps, all game graphics—including complex logic gate structures (**AND, OR, NOT, XOR, NAND, NOR**)—are drawn on-the-fly using mathematical coordinate rendering geometry ($dx^2 + dy^2 \le r^2$).

### 4. Advanced Game Mechanics
* **Fog-of-War System:** Uses a 15-bit internal memory register array (`visited_rooms`) to dynamic-mask unexplored chambers, only revealing adjacent map rooms upon grid line boundary crossing.
* **Boolean Path Routing:** Gate checkpoints analyze the player’s charge (`SW[5]`) against randomized structural environments. If the local Boolean function evaluates to `0`, coordinate registers freeze, and the timer suffers an instant **10-second penalty forward jump**.
* **Labyrinth Reflex Matrix:** The final quadrant introduces a specialized green maze pathway requiring tight, boundary-bounded coordination parameters to reach the final cell.

---

## 🚀 Compilation & Synthesis Deployment
This project was compiled, verified, and synthesized using **Intel Quartus Prime (Standard Edition)**.

### Prerequisites
* **Hardware:** Terasic DE1-SoC Development Kit (Cyclone V 5CSEMA5F31C6)
* **Software:** Intel/Altera Quartus Prime Lite Edition (Version 25.1 for Windows)
* **Language Standard:** IEEE 1800-2017 (SystemVerilog)

## 👥 Team PENTAGATES

| Team Member | Academic ID |
| :--- | :--- |
| **Melih Vatansever** | 2210357029 | 
| **Müzeyyen Beyza Tutak** | 2210357069 |
| **Ömer Soysal** | 2210357086 |
| **Elif Sude Can** | 2210357089 | 
| **Muhammed Emir Yağmur** | 2210357095 | 

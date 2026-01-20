# 128-bit SRAM Layout & Physical Verification

**Tech Stack:** Cadence Virtuoso Layout XL, Pegasus (DRC/LVS), Quantus (Extraction)  
**Process Node:** 45nm CMOS (GPDK045)  
**Course:** EE 577A - VLSI System Design

## 📌 Project Overview
This project focuses on the **physical design (Layout)** of a 128-bit SRAM array. Following the schematic design from Part A, the layout was implemented using a **hierarchical, pitch-matched abutment strategy** to ensure density and scalability.

The design was verified using **Pegasus DRC/LVS** and achieved a fully clean sign-off status with **zero design rule violations**.

## 🏗️ Layout Architecture
The design is built up from a single standard bit-cell to a full bank using a bottom-up approach.

### 1. Hierarchical Building Blocks
* **Standard Cell (`SRAM_1BIT_Layout`):** A custom 6T bit-cell layout optimized for horizontal and vertical abutment.
* **Core Array (`SRAM_2X2_Layout`):** A tiled array demonstrating shared power rails (VDD/GND) and pitch-aligned bit-lines.
* **Top Level (`SRAM_4Banks_Layout`):** The complete integration of the core array with peripherals.

### 2. Peripheral Integration
All peripheral layouts were pitch-matched to the core array to allow for direct connection without complex routing channels.
* **`Row Decoder_Layout`**: Pitch-matched to the word-lines of the core array.
* **`Precharge_Layout`**: Vertically aligned with the bit-lines.
* **`Sense Amplifier_Layout`**: Differential sensing layout aligned with the column outputs.
* **`Write Driver Layout`**: Integrated column driving logic.

## 🔎 Verification Status (DRC & LVS)
The design passed all physical verification checks using **Cadence Pegasus**.

| Cell Name | DRC Status | LVS Status |
| :--- | :--- | :--- |
| **SRAM_1BIT** | ✅ Clean (0 Errors) | ✅ Match |
| **Row Decoder** | ✅ Clean (0 Errors) | ✅ Match |
| **Sense Amplifier** | ✅ Clean (0 Errors) | ✅ Match |
| **Write Driver** | ✅ Clean (0 Errors) | ✅ Match |
| **Full Bank Top** | ✅ Clean (0 Errors) | ✅ Match |

> *See `verification_logs/` for detailed Pegasus reports showing "Total DRC Results: 0".*

## ⚡ Performance Summary
Post-layout extraction was performed using **Quantus QRC** to analyze the impact of parasitic capacitance and resistance.

| Metric | Measured Value |
| :--- | :--- |
| **Total Area** | *[Insert Area from Report] µm²* |
| **Max Clock Freq** | *[Insert Freq from Report] GHz* |
| **Read Power** | *[Insert Power] µW* |
| **Write Power** | *[Insert Power] µW* |

## 🧪 Functional Testing
The extracted netlist was simulated to verify read/write operations with full parasitics.
* **Test Sequence:** Sequential Write/Read of 10 data values.
* **Result:** Successful data retention and retrieval confirmed in Post-Layout Simulation.

## 🛠️ Tools Used
* **Layout Editor:** Cadence Virtuoso Layout XL
* **Physical Verification:** Cadence Pegasus (DRC, LVS)
* **Parasitic Extraction:** Cadence Quantus
* **Simulation:** Spectre

---
*Note: This repository contains layout screenshots and verification logs. GDSII files are excluded due to NDA/licensing restrictions.*

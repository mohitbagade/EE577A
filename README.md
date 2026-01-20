# EE577A

![giphy (5)](https://github.com/user-attachments/assets/d4af41d7-4177-4f5b-a5ad-cc6eaf40b032)


# 512-bit SRAM Array Design (45nm CMOS)

**Tech Stack:** Cadence Virtuoso, Spectre Simulation, 45nm CMOS Technology  
**Type:** Custom Full-Custom VLSI Design  
**Date:** Spring 2024

## 📌 Project Overview
This project involves the complete schematic design and characterization of a **512-bit Static Random Access Memory (SRAM)** array. Designed in a **45nm process technology** with a supply voltage of **1.0V**, the memory is organized into four interleaved banks to optimize layout and access efficiency.

The design spans from the transistor-level sizing of the 6T bit-cell to the integration of peripheral circuits, including row decoders, column selectors, sense amplifiers, and write drivers.

## ⚡ Key Features
* **Capacity:** 512 bits (32 words $\times$ 16 bits).
* **Architecture:** 4-Bank Interleaved Architecture (128 bits per bank).
* **Bit-Cell:** Standard 6T SRAM cell with custom transistor sizing for noise margin optimization.
* **Peripherals:**
    * **Row Decoder:** 3-to-8 Decoder with optimized logical effort.
    * **Sense Amplifier:** Differential voltage sensing with enable control (activates at 80-100mV $\Delta V$).
    * **Column Mux:** pMOS pass transistors for Read / nMOS pass transistors for Write.
* **Process:** 45nm CMOS ($V_{DD} = 1.0V$).

## 📐 Architecture Details

### 1. Memory Organization
The 512-bit array is split into **four banks** of 128 bits each. The 16-bit data word is **bit-interleaved** across these banks to streamline the column multiplexing and driver routing:
* **Bank 1:** Bits [15:12]
* **Bank 2:** Bits [11:8]
* **Bank 3:** Bits [7:4]
* **Bank 4:** Bits [3:0]

### 2. 6T Bit-Cell Sizing
The bit-cell transistors were manually sized to meet strict Static Noise Margin (SNM) constraints verified via butterfly curve simulations:
* **Read SNM:** $\ge$ 200 mV
* **Write SNM:** $\ge$ 395 mV

### 3. Sense Amplifier
A latch-based differential sense amplifier was implemented to detect small voltage swings on the bit-lines (BL/BLB).
* **Specification:** The Sense Enable (`sense_en`) signal triggers only after a developed voltage difference of **80–100mV** to minimize read delay while preventing false switching.
* **Precharge:** Bit-lines are precharged to 0.95 $V_{DD}$ before every operation.

## 🛠️ Circuit Schematics & Components

| Component | Description |
| :--- | :--- |
| **Row Decoder** | A 3-to-8 decoder utilizing pre-decoding logic to drive the Word Lines (WL). Includes pulse shaping to turn off WL after discharge to save power. |
| **Column Mux** | Separated Read (pMOS) and Write (nMOS) multiplexers to optimize signal integrity during operations. |
| **Write Driver** | Drives the bit-lines to Ground/VDD depending on the input data during write cycles. |
| **Output Latch** | Registers the 16-bit output data synchronized with the system clock. |

## 📊 Performance & Characterization
The design was validated using **Cadence Spectre** simulations. The following metrics were characterized:

### 1. Static Noise Margins (Butterfly Curves)
*(Insert your SNM Butterfly Curve image here - e.g., 'docs/SNM_Butterfly_Curves.png')*
* **Read Stability:** Verified via holding voltage measurements during read disturbance.
* **Write Ability:** Verified via bit-flipping threshold analysis.

### 2. Timing Analysis
* **Precharge Delay:** Time to charge BL/BLB to 0.95 $V_{DD}$.
* **Decoder Delay:** Propagation delay from Address Input to Word Line activation.
* **Sense Amp Delay:** Time from `sense_en` activation to resolved output.
* **Total Read/Write Access Time:** Measured from the rising edge of CLK to valid Output.

## 🧪 Functional Verification
The array was tested using a vector file to perform sequential Read/Write operations.
* **Test Pattern:** Sequential write of 10 values (based on USC ID) followed by sequential read verification.
* **Waveforms:** Validated correct `Write 1` $\to$ `Read 1` $\to$ `Write 0` $\to$ `Read 0` transitions.

## 📚 Course Context
**Course:** EE 577A - VLSI System Design (USC, Spring 2024)  
**Focus:** Full-custom IC design flows, memory circuit design, and timing closure in deep sub-micron technologies.

## 📈 Results Summary

### 1. Stability & Noise Margins
The SRAM bit-cell was sized and characterized to meet strict Static Noise Margin (SNM) constraints to ensure data stability during read operations and successful flipping during write operations.

| Metric | Constraint | Measured Value | Status |
| :--- | :--- | :--- | :--- |
| **Read SNM** | $\ge$ 200 mV | **[Insert Value] mV** | ✅ Pass |
| **Write SNM** | $\ge$ 395 mV | **[Insert Value] mV** | ✅ Pass |
| **Precharge Level** | $\ge$ 0.95 $V_{DD}$ | **[Insert Value] V** | ✅ Pass |

### 2. Timing Performance
Total access times were measured from the rising edge of the Clock (CLK) to the valid output at the Register. 

| Operation | Total Delay |
| :--- | :--- |
| **Read Access Time** | **[Insert Value] ps** |
| **Write Access Time** | **[Insert Value] ps** |

> **Note:** The Write delay is confirmed to be less than or equal to the Read delay, satisfying the design requirement.

### 3. Critical Path Breakdown (Read Operation)
A detailed breakdown of the read cycle was performed to identify the latency contribution of each stage.

| Stage | Delay Contribution | Description |
| :--- | :--- | :--- |
| **Decoder Delay** | **[Insert Value] ps** | Time from Address Input $\to$ Word Line (WL) Activation. |
| **Bit-Line Discharge** | **[Insert Value] ps** | Time for BL/BLB to develop $\Delta V \approx 80\text{-}100\text{mV}$. |
| **Sense Amp Delay** | **[Insert Value] ps** | Time from `sense_en` activation $\to$ Output Resolution. |

---

### 📝 Characterization Notes
* **Technology Node:** 45nm CMOS
* **Supply Voltage ($V_{DD}$):** 1.0 V
* **Sensing Threshold:** The Sense Amplifier enable signal (`sense_en`) was timed to trigger only after a developed bit-line differential of **80–100 mV**.
* **Write Driver:** N-MOS pass transistors were utilized for the column write mux to ensure strong "0" passing.

---
*Note: This repository contains documentation and schematic overviews. Full design files (Cadence libraries) are not included due to licensing restrictions.*

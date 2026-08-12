# Ultra-Low Power PMIC LDO Design & Testbench

This repository contains the full Cadence Virtuoso design files, schematics, netlists, and testbenches for the Power Management Integrated Circuit (PMIC) Low-Dropout (LDO) Regulator module, targeted for ultra-low-power wearable applications (Smart Ring Project).

---

## 📌 1. Project Overview & Architecture

The PMIC sub-system is engineered to provide a stable, low-noise power supply ($1.8\text{V}$) from a $3.3\text{V}$ input source. It features a dual-loop architecture enabling deep-sleep operation with ultra-low quiescent current ($I_q \approx 12.5\mu\text{A}$) while delivering high transient response performance during active load states.

### Core Modules Breakdown

*   **`PMIC_tb` (Top-Level Testbench):** 
    *   The top-level simulation setup used to verify integrated system-level performance, including DC operating points, transient load response, active/sleep power consumption, and Monte Carlo yield analysis.
*   **`Bandgap` (Bandgap Voltage Reference - BGR):** 
    *   Generates a stable, temperature-compensated reference voltage ($V_{ref} \approx 1.204\text{V}$) for the error amplifier and internal biasing networks.
*   **`Error_Amp_for_LDO_pmos` (Error Amplifier):** 
    *   High-gain, low-power error amplifier designed to drive the main PMOS power transistor and regulate the output voltage against line and load variations.
*   **`LDO_FVF+SSF` (Flipped Voltage Follower & Super Source Follower):** 
    *   The primary low-drop-out regulation core incorporating an FVF structure for fast transient load response and enhanced stability without requiring large external decoupling capacitors.
*   **`LDO_KeepAlive` (Keep-Alive Auxiliary Regulator):** 
    *   Ultra-low-power auxiliary regulator active during deep-sleep mode (`EN = 0V`) to maintain internal bias nodes and prevent logic state corruption.

---

## 📁 2. File Organization & Contents

Each module subfolder contains the full OpenAccess (OA) database view along with exported simulation assets:
*   **Circuit Netlists:** Raw SPICE/Spectre netlists (`.scs` / `.cdl`).
*   **Simulation Data:** Raw wave/DC data and evaluation states.
*   **Module README:** Detailed individual test cases and specific sub-circuit performance metrics are documented in a dedicated `README.md` within each folder.

---

## 🛠️ 3. Quick Start & Cadence Virtuoso Setup

To import and run these designs in your local Cadence Virtuoso environment:

1.  **Add Library to `cds.lib`:**
    Directly copy or link the sub-folders (or the parent `PMIC_LDO` directory) into your local Cadence library path. Add the following entry to your project's `cds.lib` file:
    ```text
    DEFINE PMIC_LDO ./path_to_repository/PMIC_LDO
    ```
2.  **Open Testbench:**
    Launch Cadence Virtuoso, open `PMIC_LDO -> PMIC_tb -> schematic`, and load the corresponding ADE XL / ADE Assembler state to rerun system-level simulations.

---

## ⚠️ Note on PDK Requirements
*   **Process Node:** TSMC 40nm CMOS Technology.
*   **Models Required:** Make sure your `Model Library Setup` includes statistical models (`top_ttg_localmc` or equivalent) if re-running Monte Carlo mismatch simulations.

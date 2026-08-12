# Ultra-Low-Power Dual-Loop PMIC Design Portfolio

Welcome to the design documentation and performance portfolio for a custom Ultra-Low-Power Power Management IC (PMIC). This project was designed and verified during my internship, specifically targeted at space-constrained and battery-sensitive wearable applications (e.g., Smart Rings). 

> **🛡️ IP Protection Notice:** 
> To protect proprietary company intellectual property and PDK data, this repository contains **only architectural documentation, design rationale, and performance analysis reports**. Raw Cadence OpenAccess databases, schematics, and netlists have been strictly excluded.

---

## 📊 System-Level Performance & Full Evaluation
For the comprehensive evaluation of the integrated system, including Monte Carlo yield analysis, ultra-low deep-sleep quiescent current ($I_q$), load step transient responses, and known engineering trade-offs, **please refer to the top-level testbench report:**
👉 **[PMIC_tb (Top-Level Testbench)](./PMIC_tb/README.md)**

---

## 🧩 Project Architecture & Module Directory

This PMIC leverages an innovative **Dual-Loop Architecture** to resolve the fundamental conflict between nano-ampere standby power and microsecond-level transient response. The project is modularized into 5 core sub-directories, each detailing the specific design rationale and limit testing for that block:

### 1. `PMIC_tb` (System Integration & Testbench)
*   **Role:** The top-level verification environment where all sub-modules are integrated.
*   **Content:** Contains the primary system-level reports, proving the overall functionality, global power consumption, and closed-loop stability across various operational modes (Active vs. Deep Sleep).

### 2. `LDO_FVF+SSF` (Active Power Core)
*   **Role:** The main Low-Dropout (LDO) regulator power stage active during high-workload states.
*   **Content:** Details the Flipped Voltage Follower (FVF) and Super Source Follower (SSF) architecture, which achieves gigahertz-level internal bandwidth and ultra-fast transient responses entirely **without external decoupling capacitors**.

### 3. `Error_Amp_for_LDO_pmos` (Active Error Amplifier)
*   **Role:** The primary control engine driving the FVF power stage.
*   **Content:** Explores the source-degenerated differential amplifier design. It highlights the strict 20µA current budget limitation, sleep-mode cut-off logic, and how its slew-rate limitations dictate the system's cold-start behavior.

### 4. `LDO_KeepAlive` (Deep Sleep Auxiliary LDO)
*   **Role:** A dedicated nano-ampere regulator that seamlessly takes over during the system's deep-sleep mode to maintain a 1.8V retention voltage for digital logic.
*   **Content:** Showcases a minimalist 5-transistor OTA and mega-ohm feedback network designed to burn only **350 nA** of intrinsic quiescent current while remaining unconditionally stable.

### 5. `Bandgap` (Precision Voltage Reference)
*   **Role:** The "heart" of the PMIC, providing a stable, temperature-compensated 1.2V reference voltage to the error amplifiers.
*   **Content:** Analyzes the op-amp clamped Bandgap Reference (BGR) architecture, highlighting its startup circuit robustness, loop stability (STB), and excellent Temperature Coefficient (TC) across extreme thermal ranges.

---

## 🛠️ Tech Stack & Methodologies
* **Process Node:** TSMC 40nm CMOS Technology
* **EDA Tools:** Cadence Virtuoso, ADE XL / Assembler
* **Analysis Performed:** AC (Bode/STB), DC (Sweep/ICMR), Transient (Load Step/Startup), Statistical (Monte Carlo Process & Mismatch).

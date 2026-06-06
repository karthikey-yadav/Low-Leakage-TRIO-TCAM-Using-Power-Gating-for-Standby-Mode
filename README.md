Here is a clean, comprehensive, and production-ready `README.md` file tailored specifically for your GitHub repository based on your Phase-II B.Tech project report.

---

# Low-Leakage TRIO-TCAM Using Power Gating for Standby Mode

An energy-efficient enhancement of the **10T TRIO-TCAM** architecture using a **coarse-grained Dual-Sleep Power-Gating technique** implemented in **90nm CMOS technology**. This design introduces simultaneous supply and ground isolation to drastically suppress standby leakage power while preserving high-speed parallel search functionality and robust ternary data retention.

---

## 📌 Project Overview

Ternary Content-Addressable Memory (TCAM) is a cornerstone of high-speed hardware lookup search engines (e.g., network routers, firewalls, and AI pattern-matching accelerators). However, deep sub-micron technology scaling causes exponential growth in static leakage currents ($I_{sub}$, gate-oxide, and junction leakage), making standby power a dominant energy bottleneck.

This project addresses the challenge by integrating a block-level **Dual-Sleep (Header + Footer) Configuration** into the ultra-compact **10-Transistor (10T) Triple-State-In-Cell (TRIO-TCAM)** architecture.

### Key Highlights

* **~80% Standby Leakage Reduction** (Average drop from $0.361\text{ nW}$ to $0.05\text{ - }0.08\text{ nW}$).
* **Negligible Search Delay Penalty** ($<2\%$ active search degradation).
* **Robust Ternary Data Retention** (Maintains stable storage of `0`, `1`, and `X` states in Drowsy Mode via a Data Retention Voltage $V_{DR} \approx 250\text{ mV}$).
* **Low Area Overhead** ($<5\%$ block-level area penalty by avoiding fine-grained per-cell gating arrays).

---

## 📐 Architecture & Core Components

### 1. The 10T TRIO-TCAM Cell Structure

The baseline architecture utilizes a compact 10-transistor triple-state structure mapping ternary logic states via four internal complementary nodes ($A$, $A_b$, $B$, $B_b$):

* **State '0':** $A=0, B=1, A_b=1, B_b=0$
* **State '1':** $A=1, B=0, A_b=0, B_b=1$
* **State 'X' (Don't Care):** $A=1, B=1, A_b=0, B_b=0$

### 2. Dual-Sleep Power-Gating Scheme

Instead of traditional single-switch architectures, the proposed circuit introduces:

* **PMOS Header Transistor (High-$V_T$):** Isolates the cell array from the global power supply rail ($V_{DD}$), creating a **Virtual Supply Rail ($V_{VDD}$)**.
* **NMOS Footer Transistor (High-$V_T$):** Isolates the array from true ground ($V_{SS}$), creating a **Virtual Ground Rail ($V_{VGND}$)**.

> 💡 **The Stack Effect:** Dual isolation forces structural voltage transitions along internal storage paths during standby—decreasing the overall drain-to-source voltage ($V_{DS}$) and mitigating Drain-Induced Barrier Lowering (DIBL).

---

## 📊 Performance Matrix & Simulation Results

Circuit-level transient and corner analyses were executed using **Cadence Virtuoso** in standard **90nm CMOS process parameters**.

### Core Performance Metrics

| Parameter | Baseline TRIO-TCAM | Proposed Dual-Sleep TRIO-TCAM |
| --- | --- | --- |
| **Cell Area ($\mu m^2$)** | $0.554$ | $\approx 0.58$ |
| **Energy per Bit (Active, fJ)** | $0.064 - 0.22$ | $0.07 - 0.25$ |
| **Standby Leakage Power (nW)** | $0.361$ | **$0.05 - 0.08$** |
| **Average Leakage Reduction** | Baseline | **~80%** |
| **Active Search Delay Penalty** | Baseline | **$<2\%$** |
| **Wake-Up Latency** | — | $\sim 5\text{ Clock Cycles}$ |

### Process Corner Analysis (Robustness Check)

| Process Condition | Leakage (Baseline) | Leakage (Dual-Sleep) | Leakage Reduction (%) | Search Delay (ns) |
| --- | --- | --- | --- | --- |
| **Fast Corner (FF)** | $0.48\text{ nW}$ | $0.09\text{ nW}$ | **81.0%** | $0.82\text{ ns}$ |
| **Typical Corner (TT)** | $0.361\text{ nW}$ | $0.07\text{ nW}$ | **80.0%** | $0.85\text{ ns}$ |
| **Slow Corner (SS)** | $0.27\text{ nW}$ | $0.05\text{ nW}$ | **81.5%** | $0.92\text{ ns}$ |

---

## 📂 Repository Directory Structure

```text
├── schematics/             # Circuit diagrams & Cadence Virtuoso cell views
│   ├── trio_tcam_core.png  # Base 10T TRIO-TCAM topology schematic
│   └── dual_sleep_pg.png   # Integrated dual-sleep block gating layout
├── simulations/            # Netlists, corner parameters, and testbenches
│   ├── testbench.scs       # Spectre simulation stimulus setup
│   └── waveforms/          # Active-to-Standby transition waveforms (.csv/.png)
├── docs/                   # Academic documentation and references
│   └── Project_Report.pdf  # Comprehensive Phase-II Thesis Report
└── README.md               # Repository orientation guide

```

---

## 🚀 Future Scope of Work

* **Advanced Node Optimization:** Scaling the structural design down to sub-45nm technology nodes, FinFET, or Gate-All-Around (GAA) architectures.
* **Adaptive Voltage Scaling:** Implementing a closed-loop dynamic sensor circuit to alter retention limits based on real-time temperature fluctuations.
* **System-on-Chip (SoC) Mapping:** Integrating the array module inside standard Network Intrusion Detection Systems (NIDS) pipeline benchmarks.

---

## 🧑‍💻 Project Collaborators & Framework

* **Developers:** Somisetty Indrani, Pulimamidi Sriya, Maccha Vishal Rao
* **Academic Supervisor:** Dr. Sangeeta Singh (Assistant Professor)
* **Institution:** Vardhaman College of Engineering (VCE), Hyderabad
* **Department:** Electronics and Communication Engineering (ECE)
* **Timeline:** Phase-II Project Framework (2025 - 2026 Academic Year)

---

## 📜 Citation & Bibliography

If you use this model or refer to the structural methodology in an academic context, please cite the foundational architecture work:

```bibtex
@article{trio_tcam_2024,
  author={Nguyen, T. D. and Chatterjee, P. and Kim, K. A.},
  journal={IEEE Transactions on Very Large Scale Integration (VLSI) Systems},
  title={TRIO-TCAM: A novel area- and energy-efficient TCAM architecture using a 10-transistor SRAM cell},
  year={2024},
  volume={32},
  number={4},
  pages={645-656}
}

```

# Power & Harmonic Synchronization Bus (HS-BUS)

## 🧠 Purpose

The Harmonic Synchronization Bus (`HS-BUS`) is the **timing and power coordination backbone** for the entire IX-Godelian-Harmonic-Framework.

It ensures:
- **Power delivery** remains phase-aligned across all subsystems (R1, G1, Z1, T1, S1)
- **Waveform triggers** stay harmonically locked to 3-6-9 master clocking
- **Modulation, correction, and telemetry events** remain causally safe

This is the **core nervous system** of the machine.

---

## 🔗 Synchronization Targets

| Subsystem | Phase-Sync Required | Power Timing Required |
|-----------|----------------------|------------------------|
| R1        | ✅                   | ✅                     |
| G1        | ✅                   | ✅                     |
| Z1        | ✅                   | ✅                     |
| T1        | ✅                   | Optional               |
| S1        | ✅ (coherence only)  | ❌ (passive)           |

---

## ⚙️ HS-BUS Architecture

| Layer           | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| 🧠 Master Clock   | Generates master 3-6-9 base frequency pulses                                 |
| 🕸️ Distribution Bus | Routes synchronized timing signals to all coil drivers                     |
| 🧱 Phase Buffers  | Apply programmable delay or phase offset to align signal timing              |
| 🔋 Power Lines    | Carry power from central PSU (isolated rails per subsystem)                 |
| 🎚️ Sync Taps      | Optical or digital trigger outputs for waveform generators, G1 injections   |

---

## 🧮 Master Clocking Formula

### Harmonic Timing Reference:

```math
T_n = \frac{1}{n \cdot f_0}
```

Where:
- \( T_n \) is the period of the nth harmonic (n ∈ {3, 6, 9})  
- \( f_0 \) is the base oscillator frequency (e.g., 1 Hz, 3 Hz, etc.)

All waveform-generating subsystems derive timing pulses from:

```text
Primary Sync Line → Local Phase Buffer → Modulation Trigger
```

---

## 🛠️ Real-World Components

| Component       | Recommendation                            |
|------------------|--------------------------------------------|
| Master Oscillator | Oven-controlled crystal oscillator (OCXO) |
| Signal Distributor | Star-topology buffer + shielded coax     |
| FPGA Sync Core   | Nanosecond-accurate trigger coordination   |
| PSU Isolation    | Galvanically isolated DC-DC converters     |
| Optical Triggers | For time-critical waveform start signals   |

---

## 🔌 Power Bus Logic

Each major subsystem receives **independent, harmonically-synced power delivery**:

- **R1/G1**: High-current harmonic driver rails (voltage-stabilized)
- **Z1**: Bufferable pulse rail (low ripple, high capacitance)
- **T1/S1**: Logic-level only; can share bus if isolated optically

All rails share **ground plane reference**, but each line maintains **independent switching logic** to avoid crosstalk or resonance contamination.

---

## 🧪 Sync Failure Modes & Protection

| Failure Type       | Consequence                          | Protection Mechanism                     |
|--------------------|---------------------------------------|-------------------------------------------|
| Phase Drift        | Curvature instability                 | Dynamic PLL adjustment at each node       |
| Overvoltage Ripple | Coil waveform distortion              | LC filters + isolation transformers       |
| Crosstalk Collapse | Injection field phase anomaly         | Optically decoupled modulation triggers   |
| Timing Skew        | Modulation-target mismatch            | Clock buffering + delay line calibration  |

---

## 📐 Layout Reference (Logical)

```text
[OCXO Master Clock]
       ↓
   [HS-BUS Sync Core]
       ↓ ↓ ↓ ↓ ↓
    [R1] [G1] [Z1] [T1] [S1]
       ↘      ↙
     [Waveform Generators]
```

All subsystems receive:
- Primary phase reference
- Local programmable offset (if needed)
- Isolated rail for waveform power logic

---

## 🔁 Test Recommendations

- Use square pulse test mode on master oscillator  
- Validate phase timing at each subsystem using oscilloscope or logic analyzer  
- Inject artificial skew to test G1 correction behavior

---

## 🔗 Next File: `/harmonic_injection_controller.md` – The central driver managing waveform outputs and response logic

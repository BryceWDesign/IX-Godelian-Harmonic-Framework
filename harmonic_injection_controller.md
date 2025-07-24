# Harmonic Injection Controller (HIC) – System H1

## 🧠 Purpose

The Harmonic Injection Controller (HIC), also referred to internally as `H1`, is the **central command unit** for:

- Selecting waveform modulation profiles based on telemetry data  
- Coordinating injection timing to G1 (Gankyil Modulator)  
- Validating waveform conditions against field-safe parameters  
- Ensuring phase lock across all harmonic output channels

It is the *neural switchboard* of field modulation in the IX-Godelian-Harmonic-Framework.

---

## ⚙️ Responsibilities

| Function                    | Description                                                               |
|-----------------------------|---------------------------------------------------------------------------|
| 🧠 Mode Selection           | Chooses RL, CE, CN, SR, or FR waveform mode based on current T1/G1 data   |
| ⏱️ Timing Gate              | Ensures injection occurs at correct harmonic window                        |
| 🧮 Phase Verification       | Validates that field conditions match injection profile tolerances        |
| 🚫 Conflict Arbitration     | Prevents unsafe overlap of mutually exclusive modes (e.g., CE + CN)        |
| 🔁 Feedback Conditioning    | Refines real-time modulation profile based on deviation slope              |

---

## 🔁 Input Signals

| Source | Signal                           | Purpose                                |
|--------|----------------------------------|----------------------------------------|
| T1     | `PHASE_Δ`, `CURVATURE_Δ`         | Detects instability or field drift     |
| S1     | `S1_VECTOR_ANGLE`                | Assists in directional waveform tuning |
| Z1     | `Z1_TRIGGER`                     | Avoids injection during ERP overlap    |
| G1     | `G1_RESPONSE_LATENCY` (optional) | Feedback performance timing            |

---

## 🔀 Waveform Selection Logic

### Default State: Resonant Lock (RL)

HIC maintains `RL` mode unless one or more of the following thresholds are exceeded:

```text
if (CURVATURE_Δ > 3.0°) → enter CE mode
if (CURVATURE_Δ > 6.5°) && (PHASE_Δ > 0.18) → enter CN mode
if (PHASE_Δ drifts continuously > 0.05 rad over 3 cycles) → enter SR mode
if (G1_MODE == CN) → schedule FR mode after 1 cycle
```

Each state transition is timestamped and logged into `T-log`.

---

## ⏲️ Injection Timing

All waveform injections are synchronized to HS-BUS master clock:

```math
t_{\text{inject}} = t_0 + k \cdot T_{sync}
```

Where:
- \( T_{sync} \) is the synchronization interval (e.g. 111 ms for 9 Hz)  
- \( k \) ∈ ℕ is the injection step index

---

## 📦 Implementation Notes

- HIC can be implemented in FPGA, microcontroller, or hybrid digital logic  
- Response latency should remain below 2 ms for effective pre-collapse response  
- Suggested fallback: Default to `RL` if telemetry signal is lost >500 ms

---

## 🧰 Real-World Components

- FPGA (e.g., Xilinx Spartan or Lattice ICE40)  
- Optional: Analog comparator backup logic for low-level fallback  
- Isolated I/O lines for injecting pulse triggers to G1 waveform generator  
- Direct connection to T1/S1 output buffers and HS-BUS sync tap

---

## 🔐 Safety Parameters

| Safety Constraint                     | Threshold                             |
|--------------------------------------|----------------------------------------|
| Max curvature correction per second  | 12°                                    |
| Max phase delta injection per cycle  | 0.25 radians                           |
| Minimum delay between mode switches  | 111 ms (one full 9 Hz base cycle)      |
| ERP suppression window (Z1 overlap)  | Do not inject during Z1 active pulse   |

---

## 📊 Output Events

HIC logs all injections, mode changes, timing anomalies, and suppression events to the `T-log` stream using the following codes:

```text
[MODE_CHANGE] [MODE] [REASON] [TIMESTAMP]
[INJECTION_OK] [MODE] [t_inject] [Δθ] [Δφ]
[SUPPRESSED] [REASON] [Z1_ACTIVE / BAD_Δ]
```

---

## 🔗 Next File: `/safety_interlock_matrix.md` – Coordinated system-wide protection logic against timing or energy misuse

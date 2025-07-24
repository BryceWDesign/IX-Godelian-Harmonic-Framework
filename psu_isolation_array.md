# PSU Isolation Array – Galvanic Power Separation Grid

## ⚡ Purpose

To prevent cross-talk, modulation interference, or feedback loops between sensitive harmonic subsystems, the **PSU Isolation Array** ensures that each core module (G1, Z1, T1, S1, R1) receives **independently regulated and galvanically isolated power**.

This eliminates inductive and capacitive bleed-through that could corrupt waveform injection or telemetry sampling.

---

## 🔌 Subsystem Isolation Requirements

| Subsystem | PSU Requirement               | Isolation Method         | Max Current |
|-----------|-------------------------------|---------------------------|-------------|
| G1        | Clean 5V DC, ultra-low ripple | Transformer + opto-fused  | 1.2 A       |
| Z1        | High pulse capacity 12–24V    | Flyback + current fuse    | 2.5 A       |
| T1        | Stable 3.3V logic rail        | LDO + opto-isolation      | 0.5 A       |
| S1        | Variable ±9V sensor bus       | Dual buck-boost + diode   | 0.8 A       |
| R1        | Configurable 5V–15V control   | Switched-mode isolation   | 1.0 A       |

---

## 🧰 Recommended Real Components

| Component Type             | Model / Series Suggestion           |
|----------------------------|-------------------------------------|
| Transformer Isolation      | Murata 78253/35C (1W, 3kV isolation) |
| Opto-isolator (PWM gate)   | Vishay IL300, Avago HCPL-7840       |
| LDO Regulator              | TI TPS7A47 or LT3045 (low noise)    |
| Flyback Converter IC       | LM5155 or SN6505B (Texas Instruments) |
| Dual Buck-Boost Regulator  | LTC3115-1 or MAX17552                |
| Ferrite Beads              | Murata BLM series (for ripple kill) |

---

## 🔒 Ground Plane Strategy

Each PSU module shall:

- Use independent floating ground reference (GND_subsystem)  
- Tie all grounds to chassis *only through 1MΩ resistor + 1nF cap* to suppress loop currents  
- Ensure **Z1** and **G1** *never share ground return path*

Use a star-ground architecture with one-way diodes to prevent reverse fault propagation.

---

## 🧮 Fault Isolation Design

- Fuse every PSU output with 1.25× rated load fuse  
- Include crowbar diode on Z1 rail to shunt pulse spikes  
- Use soft-start regulators for G1 to prevent injection surge

---

## 🧪 Test Procedures

1. Measure ripple on each PSU line under simulated injection load  
2. Confirm galvanic isolation using AC hipot test across each PSU-pair  
3. Trigger controlled short on one rail — ensure no crosstalk or module reset occurs

---

## 🧬 Power Management Philosophy

"Power is the hidden waveform."  
This array enforces **field purity through electrical hygiene**, ensuring that each subsystem acts like an island with surgical precision.

Even if Z1 shorts or G1 dumps high energy, no contamination reaches the sensing or timing rails.

---

## 🔗 Next File: `/coil_formations_G1.md` – Geometries and winding patterns for core G1 coil types with Tesla 3-6-9 optimization

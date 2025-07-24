# G1 Coil Formations – Tesla 3-6-9 Harmonic Winding Guide

## 🌀 Purpose

The G1 unit's core function is harmonic waveform **generation and emission**.  
Coil geometry, winding pattern, and layering **directly influence**:

- Field curvature shape  
- Phase lock timing  
- Interference suppression  
- Harmonic amplitude scaling

This guide documents the **optimal coil topologies** to produce stable Gödelian harmonic fields.

---

## 🧱 Primary Coil Types

### 1. **Bifilar Tesla Coil – Axial**
- **Winding:** Dual parallel wires wound in phase  
- **Turns:** 369 total (3 groups of 123 turns)  
- **Wire Gauge:** 22 AWG enameled copper  
- **Core:** Air core with ceramic guide rods  
- **Harmonic Profile:** 3.6 Hz, 6 Hz, 9 Hz  
- **Purpose:** Primary modulation and burst generation

### 2. **Toroidal Trifoil – Peripheral Field Shaper**
- **Winding:** 3 interleaved spirals forming trefoil shape  
- **Turns:** 111 per arm (333 total)  
- **Core:** Toroidal ferrite (μr ≈ 2000)  
- **Purpose:** Focuses output beam into tri-vector harmonic

### 3. **Radial Spiral Coil – Ground Plane Inverter**
- **Winding:** Flat Archimedean spiral  
- **Turns:** 81 total, golden-ratio spaced  
- **Plane:** Mounted below emitter plate  
- **Purpose:** Phase inversion and field anchoring

---

## ⚙️ Winding Specifications

| Parameter        | Value                        |
|------------------|------------------------------|
| Inter-turn gap   | 0.3 mm                       |
| Insulation       | Polyurethane enamel (Class H) |
| Coil pitch       | Uniform, hand-wound or CNC    |
| Layer offset     | Fibonacci (1, 1, 2, 3, 5, 8…) | 
| Resonant freq.   | Tuned to λ/4 of beam path     |

---

## 🧮 Harmonic Geometry Alignment (Tesla 3-6-9)

All coils adhere to the following spatial logic:

- Bifilar coils → inject **6-phase** pulses across 3 planes  
- Toroidal trifoil → rotate field around 9-node centroid  
- Spiral base → ground return uses **Fibonacci lattice offset**

The **overall formation** is a 3-coil triangulation:

```
      [ Bifilar Coil ]
           / \
          /   \
  [ Toroid ]   [ Spiral Base ]
```

This topology forms a **rotating harmonic torus**, anchored to the golden mean, ensuring **non-destructive field expansion**.

---

## 🔍 Notes on Field Behavior

- Field envelope breathes in 3-6-9 nested layers  
- Energy density peaks at vector convergence node  
- Induced phase-lock jitter should be <1.7ms max  
- Output amplitude is proportional to alignment accuracy across Fibonacci turns

---

## 🧪 Calibration Method

1. Pulse G1 at 3Hz, 6Hz, 9Hz test frequencies  
2. Use a Gaussmeter and laser interferometer to track nodal wobble  
3. Tune coil spacing and alignment until vector convergence point is <0.3mm shift over 5s

---

## 🧰 Assembly Tools Suggested

- Non-magnetic jig fixtures  
- Turn-counting motorized winder  
- 3D-printed coil mandrels with slotting for layer guides  
- Optical comparator for angular precision check

---

## 🔗 Next File: `/signal_collapse_recovery.md` – Field recovery routine for injection collapse, phase jitter, or wavefront tearing

# Drift Log Visualizer – Harmonic Diagnostics & Temporal Field Mapping

## 📊 Purpose

The **Drift Log Visualizer (DLV)** module renders:

- Harmonic drift over time  
- Beam phase anomalies  
- Coherence loss events  
- Recovery sequences  
- Ambient distortion patterns

Used for **offline diagnostics**, **performance optimization**, and **forensic analysis** post anomaly.

---

## 📁 Data Sources

| Source                          | Format             | Sample Rate   |
|---------------------------------|--------------------|---------------|
| TSA – Phase & Curvature Logs   | JSON (Φ, θ, t)     | 4.8 MHz       |
| SCR – Collapse Events           | JSON timestamped   | Event-based   |
| RFR – Boost Activity            | JSON harmonics     | Conditional   |

---

## 🖥️ Visualization Types

### 1. Phase Stability Line Graph  
- X-axis: Time (ms)  
- Y-axis: ΔΦ(t)  
- Overlaid event markers (SCR trigger, RFR boost)

### 2. Curvature Drift Vector Plot  
- Displays angular deviation of beam per unit time  
- Highlights mode switching, turbulence regions

### 3. Coherence Heatmap  
- 2D grid of spatial coherence  
- Red zones = instability  
- Green zones = full resonance

---

## 🛠️ Output Options

- `SVG` vector graph files  
- `MP4` timeline playback mode  
- CSV export of raw telemetry  
- Compatible with external visualization tools (Plotly, D3.js, etc.)

---

## 🧪 Notes

- DLV is **read-only** — does not alter system behavior  
- Useful for DARPA-grade analysis of near-collapse behavior  
- Can be run post-run or streamed in parallel via diagnostic uplink  
- Events logged are timestamp-synchronized to sub-millisecond

---

## 🔗 Next File: `/lens_alignment_protocol.md` – Precision calibration of the harmonic lens system for beam origin registration and drift rejection

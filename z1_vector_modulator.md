# Z1 Vector Modulator – Curvature Pulse Driver Logic

## 🎯 Function

The **Z1 Vector Modulator** generates and modulates curvature pulses — which are time-variant distortions of spacetime field topology — through precise control over:

- Phase vector alignment  
- Pulse amplitude shaping  
- Harmonic direction rotation (clockwise / counter-clockwise modulation)  
- Gated trigger logic for synchronized injection

Z1 acts as the **steering wheel** of the Gödelian harmonic engine.

---

## ⚙️ Input Signals

| Signal | Source | Description |
|--------|--------|-------------|
| CLK_T1 | T1     | Master timing pulse for sync |
| φ(t)   | DRM    | Desired curvature phase offset |
| A_mod  | DRM    | Dynamic amplitude envelope |
| ENABLE | SIM    | Safety-verified injection flag |

---

## 📐 Output Behavior

Z1 produces a modulated output waveform:

```math
Z_out(t) = A_mod(t) · sin(φ(t) + ω·t + θ₀)
```

Where:
- \( A_mod(t) \): dynamically shaped amplitude from DRM
- \( φ(t) \): phase offset to steer curvature angle
- \( ω \): harmonic angular frequency (varies per cycle)
- \( θ₀ \): injected rotation bias (set by user)

---

## 🔁 Gating Logic

To ensure no interference or unsafe firing, Z1 only transmits if:

```pseudocode
if ENABLE == True and |φ(t)| < 180° and A_mod(t) > threshold:
    fire()
else:
    hold()
```

Gate timing is tied to T1 rising edge with optional delay:

```pseudocode
Z_fire = T1_rising + φ_offset_delay
```

---

## 🔄 Harmonic Rotation Logic

Z1 can rotate curvature injections either:

- **Clockwise**: Aligns with +θ trajectory, used for advancing phase  
- **Counter-Clockwise**: Used for phase withdrawal or recoil-mode damping

The rotation mode is toggled by bitstream control via:

```pseudocode
ROTATE_MODE = DRM.harmonic_mode
```

---

## 🧮 Amplitude Shaping Profiles

| Mode         | Description                            |
|--------------|----------------------------------------|
| Linear Ramp  | Basic energy ascent/descent            |
| Sine Envelope| Smooth wavelet-style pulse             |
| Gaussian     | Focused curvature distortion injection |
| Pulse Train  | Used for stuttered triangulation       |

Amplitude is clamped to prevent overshoot:

```pseudocode
if A_mod > MAX_SAFE:
    A_mod = MAX_SAFE
```

---

## 📊 Debug Channels

Z1 outputs telemetry to the logging bus:

- Instantaneous φ(t), A_mod(t), and ω  
- Firing events (timestamped)  
- Mode flags: rotation, gating, amplitude profile  

---

## 🧬 Integration

Z1 vector logic is coordinated by:

- `/dynamic_resonance_mapper.md` – to define φ(t) and A_mod(t)  
- `/signal_collapse_recovery.md` – to abort on unsafe vectoring  
- `/safety_interlock_matrix.md` – to enforce boundary lockout

---

## 🔗 Next File: `/gyroscopic_feedback_t1.md` – Real-time feedback loop from inertial sensors and harmonic vector correction via T1 channel

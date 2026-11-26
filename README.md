# Exp.No:6 Optical Amplifier (EDFA) Performance Analysis

## Aim

To study the gain and noise performance of an Erbium Doped Fiber Amplifier (EDFA) using Python simulation.

## Apparatus / Software Required

- Python (NumPy)
- Matplotlib
- Google Colab

## Theory

- EDFA amplifies optical signals in the C-band (1530–1565 nm) using stimulated emission.
- Gain depends on wavelength and pump power.
- Noise figure quantifies SNR degradation.

## Formulas

### 1. Gain

**Amplifier Gain:**

```text
G = P_out / P_in
```

**Gain in dB:**

```text
G_dB = 10 × log10(P_out / P_in)
```

### 2. ASE Power

```text
P_ASE = 2 × n_sp × (G - 1) × h × ν × B_o
```

Where:

- n_sp = Spontaneous emission factor
- G = Amplifier gain (linear)
- h = Planck's constant
- ν = Optical frequency
- B_o = Optical bandwidth

### 3. Noise Figure

**Noise Factor:**

```text
F = SNR_in / SNR_out
```

**For EDFA:**

```text
F = 2 × n_sp × (G - 1) / G
```

**Noise Figure in dB:**

```text
NF = 10 × log10(F)
```

For high-gain EDFAs (G >> 1):

```text
NF ≈ 10 × log10(2 × n_sp)
```

Typical commercial EDFAs have a noise figure of approximately 4–6 dB.

## Typical Practical Values

| Parameter | Typical Value |
|---|---|
| Pump wavelength | 980 nm / 1480 nm |
| Signal wavelength | 1530–1565 nm |
| Peak gain | 25–40 dB |
| Saturation output power | 10–23 dBm |
| Noise figure | 4–6 dB |
| Fiber length | 5–20 m |

## Sample Output

**Graph:** Gain spectrum curve peaking near 1550 nm.

![EDFA Output 1](https://github.com/user-attachments/assets/15e6aaff-d3f3-42d1-aa76-66bb575b6c93)

![EDFA Output 2](https://github.com/user-attachments/assets/cce70c57-34f5-4634-a90e-df47c4e45b62)

![EDFA Output 3](https://github.com/user-attachments/assets/0f298da2-0dc1-43fd-bab6-0641a5210748)

## Python Code

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
h = 6.626e-34
c = 3e8
wavelength = 1550e-9
nu = c / wavelength

# Parameters
nsp = 1.2
B = 50e9
Pin = 1e-6

# 1. Gain vs Pump Power
pump_power = np.linspace(0.01, 0.2, 50)

G_linear = 1 + 50 * (pump_power / (pump_power + 0.05))
G_dB = 10 * np.log10(G_linear)

plt.figure()
plt.plot(pump_power, G_dB)
plt.xlabel("Pump Power (W)")
plt.ylabel("Gain (dB)")
plt.title("Gain vs Pump Power")
plt.grid()
plt.show()

# 2. EDFA Gain Spectrum
wavelength_nm = np.linspace(1525, 1565, 100)

G_spec = 30 * np.exp(-((wavelength_nm - 1535) / 10)**2)

plt.figure()
plt.plot(wavelength_nm, G_spec)
plt.xlabel("Wavelength (nm)")
plt.ylabel("Gain (dB)")
plt.title("EDFA Gain Spectrum")
plt.grid()
plt.show()

# 3. Noise Figure
F = 2 * nsp * (G_linear - 1) / G_linear
NF_dB = 10 * np.log10(F)

plt.figure()
plt.plot(G_dB, NF_dB)
plt.xlabel("Gain (dB)")
plt.ylabel("Noise Figure (dB)")
plt.title("Noise Figure vs Gain")
plt.grid()
plt.show()

# 4. ASE Power
P_ASE = 2 * nsp * (G_linear[-1] - 1) * h * nu * B

print("Maximum Gain =", round(G_dB[-1], 2), "dB")
print("Noise Figure =", round(NF_dB[-1], 2), "dB")
print("ASE Power =", "{:.3e}".format(P_ASE), "W")
```

## Output

<img width="827" height="1514" alt="image" src="https://github.com/user-attachments/assets/6aae9bfa-3950-4eb9-973a-cdd3f7c00891" />
<img width="1132" height="1600" alt="image" src="https://github.com/user-attachments/assets/3ef1d654-3f39-4d63-8e0c-e38bfd113a35" />



## Result

The EDFA performance was successfully simulated using Python, and its gain, noise figure, and ASE power were analyzed.

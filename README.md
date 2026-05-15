# Ex1 : Ideal Sampling, Natural Sampling and Flat-top Sampling
## AIM:
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.

## TOOLS REQUIRED:
Python IDE

## PROGRAM:

#### IDEAL SAMPLING:
```
# Ideal Sampling

import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import resample

# Parameters
fs, f = 100, 5
t = np.arange(0, 1, 1/fs)

# Continuous signal
x = np.sin(2 * np.pi * f * t)

# Impulse sampling
xs = x

# Reconstruction
xr = resample(xs, len(t))

# Plot
plt.figure(figsize=(10, 8))
plt.suptitle(
    "NAME : UDAYAINARAYANA R\nREG NO : 212224060289",
    fontsize=12,
    fontweight='bold'
)

plt.subplot(3, 1, 1)
plt.plot(t, x)
plt.title("Continuous Signal (fs = 100 Hz)")
plt.grid(True)

plt.subplot(3, 1, 2)
plt.stem(t, xs, basefmt=" ")
plt.title("Sampled Signal (Impulse Sampling)")
plt.grid(True)

plt.subplot(3, 1, 3)
plt.plot(t, xr, 'r--')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```
#### NATURAL SAMPLING:
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs, T, fm, fp = 1000, 1, 5, 50
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Pulse train
pw = fs // (2 * fp)
p = np.zeros_like(t)
p[::fs // fp] = 1
p = np.convolve(p, np.ones(pw), mode='same')

# Natural sampling
nat = m * p

# Reconstruction (LPF)
b, a = butter(4, 10 / (0.5 * fs), 'low')
rec = lfilter(b, a, nat)

# Plot
plt.figure(figsize=(10, 9))
plt.suptitle(
    "NAME : UDAYAINARAYANA R\nREG NO : 212224060289",
    fontsize=12,
    fontweight='bold'
)

plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")
plt.grid(True)

plt.subplot(4, 1, 2)
plt.plot(t, p)
plt.title("Pulse Train")
plt.grid(True)

plt.subplot(4, 1, 3)
plt.plot(t, nat)
plt.title("Natural Sampling")
plt.grid(True)

plt.subplot(4, 1, 4)
plt.plot(t, rec, color='g')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```
#### FLAT-TOP SAMPLING:
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs, T, fm, fp = 1000, 1, 5, 50
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Sampling
bd = fs // fp
idx = np.arange(0, len(t), bd)

flat = np.zeros_like(t)

for i in idx:
    flat[i:i + bd // 2] = m[i]

# Low-pass filter (reconstruction)
b, a = butter(4, (2 * fm) / (0.5 * fs), 'low')
recon = lfilter(b, a, flat)

# Plot
plt.figure(figsize=(10, 9))
plt.suptitle(
    "NAME : UDAYAINARAYANA R\nREG NO : 212224060289",
    fontsize=12,
    fontweight='bold'
)

plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")

plt.subplot(4, 1, 2)
plt.stem(t[idx], np.ones_like(idx), basefmt=" ")
plt.title("Sampling Instants")

plt.subplot(4, 1, 3)
plt.plot(t, flat)
plt.title("Flat-Top Sampled Signal")

plt.subplot(4, 1, 4)
plt.plot(t, recon, color='g')
plt.title("Reconstructed Signal")

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```
## OUTPUT WAVEFORM:
#### IDEAL SAMPLING:
<img width="827" height="647" alt="image" src="https://github.com/user-attachments/assets/0592141e-e7ed-4d44-97e7-71234e19fd8c" />

#### NATURAL SAMPLING:
<img width="816" height="743" alt="image" src="https://github.com/user-attachments/assets/7b5422e2-25d5-483f-9d25-d8e77af5cfdc" />

#### FLAT-TOP SAMPLING:
<img width="818" height="736" alt="image" src="https://github.com/user-attachments/assets/5e4b4f61-5b06-41a1-8ff4-959b83002d19" />

## RESULT:
Thus, the construction and reconstruction of Ideal, Natural and Flat-top sampling were successfully implemented using Python, and the corresponding waveforms were obtained.

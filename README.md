# TSAF-Ex-7-Spectral-Analysis-Spectral-Density-and-Time-Invariant-Linear-Filters

## AIM:

To simulate a time series, calculate its spectral density, perform spectral analysis using
the periodogram, and study the effect of a time-invariant linear filter.

## PROGRAM:

```
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

# 1. Generate time points
n = 500
t = np.arange(n)

# 2. Generate series with 3 frequencies: 0.03, 0.12, and 0.28
x = (np.sin(2 * np.pi * 0.03 * t) +
 0.6 * np.sin(2 * np.pi * 0.12 * t) +
 0.4 * np.sin(2 * np.pi * 0.28 * t) +
 0.2 * np.random.randn(n))

# 3. Periodogram & Primary Peak
freq, power = signal.periodogram(x)
print("Primary Dominant Frequency:", freq[np.argmax(power)])

# 4. Apply 7-point Moving Average Filter
window = 7
filtered = np.convolve(x, np.ones(window) / window, mode="same")

# 5. Spectrum computation
f_orig, p_orig = signal.periodogram(x)
f_filt, p_filt = signal.periodogram(filtered)

# 6. Plot results
fig, axes = plt.subplots(2, 1, figsize=(10, 8))
axes[0].plot(t, x, label="Multi-Harmonic Input", alpha=0.6)
axes[0].plot(t, filtered, label="Filtered Output", color='red')
axes[0].set_title("Time Domain Signal")
axes[0].legend()
axes[1].plot(f_orig, p_orig, label="Original Power Spectrum")
axes[1].plot(f_filt, p_filt, label="Filtered Power Spectrum", color='red')
axes[1].set_title("Spectral Density Analysis")
axes[1].legend()
plt.tight_layout()
plt.show()
```

## OUTPUT:

<img width="837" height="682" alt="image" src="https://github.com/user-attachments/assets/32d49562-d2ec-4640-b4f0-9843dca111ef" />

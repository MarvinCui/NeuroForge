# How To: Csd Fourier

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computing cross-spectral density using short-term Fourier.

## Prerequisites

**Required Modules:**
- `pickle`
- `itertools`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne.channels`
- `mne.proj`
- `mne.time_frequency`
- `mne.time_frequency.csd`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test computing cross-spectral density using short-term Fourier.'

```python
'Test computing cross-spectral density using short-term Fourier.'
```

**Verification:**
```python
assert csd.tmin == 0 and csd.tmax == 9.98
```

### Step 2: Assign epochs = _generate_coherence_data(...)

```python
epochs = _generate_coherence_data()
```

**Verification:**
```python
assert csd.tmin == tmin and csd.tmax == tmax
```

### Step 3: Assign sfreq = value

```python
sfreq = epochs.info['sfreq']
```

**Verification:**
```python
assert abs(signal_power_per_sample - fourier_power_per_sample) < 0.001
```

### Step 4: Call _test_fourier_multitaper_parameters()

```python
_test_fourier_multitaper_parameters(epochs, csd_fourier, csd_array_fourier)
```

### Step 5: Assign times = value

```python
times = [(None, None), (1, 9)]
```

### Step 6: Assign as_arrays = value

```python
as_arrays = [False, True]
```

### Step 7: Assign parameters = product(...)

```python
parameters = product(times, as_arrays)
```

### Step 8: Assign times = value

```python
times = np.arange(20 * sfreq) / sfreq
```

### Step 9: Assign signal = value

```python
signal = np.sin(2 * np.pi * 10 * times)[None, None, :]
```

### Step 10: Assign signal_power_per_sample = value

```python
signal_power_per_sample = sum_squared(signal) / len(times)
```

### Step 11: Assign csd = csd.mean(...)

```python
csd = csd.mean([9.9, 14.9, 21.9], [10.1, 15.1, 22.1])
```

### Step 12: Call _test_csd_matrix()

```python
_test_csd_matrix(csd)
```

### Step 13: Assign t_mask = value

```python
t_mask = times <= tmax
```

### Step 14: Assign n_samples = sum(...)

```python
n_samples = sum(t_mask)
```

### Step 15: Assign csd = csd_array_fourier(...)

```python
csd = csd_array_fourier(epochs.get_data(copy=False), sfreq, epochs.tmin, fmin=9, fmax=23, tmin=tmin, tmax=tmax, ch_names=epochs.ch_names)
```

### Step 16: Assign csd = csd_fourier(...)

```python
csd = csd_fourier(epochs, fmin=9, fmax=23, tmin=tmin, tmax=tmax)
```

**Verification:**
```python
assert csd.tmin == 0 and csd.tmax == 9.98
```

### Step 17: Assign n_fft = value

```python
n_fft = n_samples + add_n_fft
```

### Step 18: Assign csd = csd_array_fourier.sum.get_data(...)

```python
csd = csd_array_fourier(signal, sfreq, tmax=tmax, n_fft=n_fft).sum().get_data()
```

### Step 19: Assign first_samp = value

```python
first_samp = csd[0, 0]
```

### Step 20: Assign fourier_power_per_sample = value

```python
fourier_power_per_sample = np.abs(first_samp) * sfreq / n_fft
```

**Verification:**
```python
assert abs(signal_power_per_sample - fourier_power_per_sample) < 0.001
```


## Complete Example

```python
# Workflow
'Test computing cross-spectral density using short-term Fourier.'
epochs = _generate_coherence_data()
sfreq = epochs.info['sfreq']
_test_fourier_multitaper_parameters(epochs, csd_fourier, csd_array_fourier)
times = [(None, None), (1, 9)]
as_arrays = [False, True]
parameters = product(times, as_arrays)
for (tmin, tmax), as_array in parameters:
    if as_array:
        csd = csd_array_fourier(epochs.get_data(copy=False), sfreq, epochs.tmin, fmin=9, fmax=23, tmin=tmin, tmax=tmax, ch_names=epochs.ch_names)
    else:
        csd = csd_fourier(epochs, fmin=9, fmax=23, tmin=tmin, tmax=tmax)
    if tmin is None and tmax is None:
        assert csd.tmin == 0 and csd.tmax == 9.98
    else:
        assert csd.tmin == tmin and csd.tmax == tmax
    csd = csd.mean([9.9, 14.9, 21.9], [10.1, 15.1, 22.1])
    _test_csd_matrix(csd)
times = np.arange(20 * sfreq) / sfreq
signal = np.sin(2 * np.pi * 10 * times)[None, None, :]
signal_power_per_sample = sum_squared(signal) / len(times)
for tmax in [12, 18]:
    t_mask = times <= tmax
    n_samples = sum(t_mask)
    for add_n_fft in [0, 30]:
        n_fft = n_samples + add_n_fft
        csd = csd_array_fourier(signal, sfreq, tmax=tmax, n_fft=n_fft).sum().get_data()
        first_samp = csd[0, 0]
        fourier_power_per_sample = np.abs(first_samp) * sfreq / n_fft
        assert abs(signal_power_per_sample - fourier_power_per_sample) < 0.001
```

## Next Steps


---

*Source: test_csd.py:448 | Complexity: Advanced | Last updated: 2026-05-18*
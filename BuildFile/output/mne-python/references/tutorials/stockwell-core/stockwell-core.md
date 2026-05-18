# How To: Stockwell Core

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test stockwell transform.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency._stockwell`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test stockwell transform.'

```python
'Test stockwell transform.'
```

**Verification:**
```python
assert_equal(st_pulse.shape[-1], len(pulse))
```

### Step 2: Assign sfreq = 1000.0

```python
sfreq = 1000.0
```

**Verification:**
```python
assert_allclose(st_max_freq, pulse_freq, atol=1.0)
```

### Step 3: Assign dur = 0.5

```python
dur = 0.5
```

**Verification:**
```python
assert onset < t[st_pulse.max(axis=0).argmax(axis=0)] < offset
```

### Step 4: Assign unknown = value

```python
onset, offset = (0.175, 0.275)
```

**Verification:**
```python
assert_array_almost_equal(pulse, y_inv)
```

### Step 5: Assign n_samp = int(...)

```python
n_samp = int(sfreq * dur)
```

### Step 6: Assign t = value

```python
t = np.arange(n_samp) / sfreq
```

### Step 7: Assign pulse_freq = 15.0

```python
pulse_freq = 15.0
```

### Step 8: Assign pulse = np.cos(...)

```python
pulse = np.cos(2.0 * np.pi * pulse_freq * t)
```

### Step 9: Assign unknown = 0.0

```python
pulse[0:int(onset * sfreq)] = 0.0
```

### Step 10: Assign unknown = 0.0

```python
pulse[int(offset * sfreq):] = 0.0
```

### Step 11: Assign width = 0.5

```python
width = 0.5
```

### Step 12: Assign freqs = fftpack.fftfreq(...)

```python
freqs = fftpack.fftfreq(len(pulse), 1.0 / sfreq)
```

### Step 13: Assign unknown = value

```python
fmin, fmax = (1.0, 100.0)
```

### Step 14: Assign unknown = value

```python
start_f, stop_f = (np.abs(freqs - f).argmin() for f in (fmin, fmax))
```

### Step 15: Assign W = _precompute_st_windows(...)

```python
W = _precompute_st_windows(n_samp, start_f, stop_f, sfreq, width)
```

### Step 16: Assign st_pulse = _st(...)

```python
st_pulse = _st(pulse, start_f, W)
```

### Step 17: Assign st_pulse = value

```python
st_pulse = np.abs(st_pulse) ** 2
```

### Step 18: Call assert_equal()

```python
assert_equal(st_pulse.shape[-1], len(pulse))
```

### Step 19: Assign st_max_freq = value

```python
st_max_freq = freqs[st_pulse.max(axis=1).argmax(axis=0)]
```

### Step 20: Call assert_allclose()

```python
assert_allclose(st_max_freq, pulse_freq, atol=1.0)
```

**Verification:**
```python
assert onset < t[st_pulse.max(axis=0).argmax(axis=0)] < offset
```

### Step 21: Assign width = 1.0

```python
width = 1.0
```

### Step 22: Assign unknown = value

```python
start_f, stop_f = (0, len(pulse))
```

### Step 23: Assign W = _precompute_st_windows(...)

```python
W = _precompute_st_windows(n_samp, start_f, stop_f, sfreq, width)
```

### Step 24: Assign y = _st(...)

```python
y = _st(pulse, start_f, W)
```

### Step 25: Assign y_inv = value

```python
y_inv = fftpack.ifft(np.sum(y, axis=1)).real
```

### Step 26: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pulse, y_inv)
```


## Complete Example

```python
# Workflow
'Test stockwell transform.'
sfreq = 1000.0
dur = 0.5
onset, offset = (0.175, 0.275)
n_samp = int(sfreq * dur)
t = np.arange(n_samp) / sfreq
pulse_freq = 15.0
pulse = np.cos(2.0 * np.pi * pulse_freq * t)
pulse[0:int(onset * sfreq)] = 0.0
pulse[int(offset * sfreq):] = 0.0
width = 0.5
freqs = fftpack.fftfreq(len(pulse), 1.0 / sfreq)
fmin, fmax = (1.0, 100.0)
start_f, stop_f = (np.abs(freqs - f).argmin() for f in (fmin, fmax))
W = _precompute_st_windows(n_samp, start_f, stop_f, sfreq, width)
st_pulse = _st(pulse, start_f, W)
st_pulse = np.abs(st_pulse) ** 2
assert_equal(st_pulse.shape[-1], len(pulse))
st_max_freq = freqs[st_pulse.max(axis=1).argmax(axis=0)]
assert_allclose(st_max_freq, pulse_freq, atol=1.0)
assert onset < t[st_pulse.max(axis=0).argmax(axis=0)] < offset
width = 1.0
start_f, stop_f = (0, len(pulse))
W = _precompute_st_windows(n_samp, start_f, stop_f, sfreq, width)
y = _st(pulse, start_f, W)
y_inv = fftpack.ifft(np.sum(y, axis=1)).real
assert_array_almost_equal(pulse, y_inv)
```

## Next Steps


---

*Source: test_stockwell.py:70 | Complexity: Advanced | Last updated: 2026-05-18*